1. для ключевых методов типа stop, start  и т.д можно делать основное тело не безопасным с точки зрения многопоточности отдельным приватным методом, и вызывать его уже более классическим методом. В этом случае можно легче вызвать методы остановки уже в защищенной секции,
   ```cpp
   class Task {
   public:
	   void Run() {
		   std::lock_guard<std::mutex> lock(mutex_);
		   runImpl();
	   }
	   void Stop() {
		   pthread_mutex_lock(&pmutex_);
		   stopImp();
		   pthread_mutex_unlock(&pmutex_);
	   }
   private:
	   //UNSAFE. Mutex has to be taken.
	   void runImpl() {
		   //Do something
		   if (something_going_wrong)
			   stopImp();
	   }
	   
	   void stopImp() {
		   //stop process
	   }
	   
	   std::mutex mutex_;
	   pthread_mutex_t pmutex_;
   };
   ```