# Threading 101

Threading allow to do parallel programming: instead of executing code linearly, we can execute snaps of code in parallel.

**Example**: Executing some code while another part of the programm download a file.

For details, see [Python.com](https://docs.python.org/2/library/threading.html).

## Basic class with treading

```Python
from threading import Thread

class ThreadFunction(Thread): # 1. The class must inherit Thread
    def __init__(self, name):
        Thread.__init__(self)
        self.name = name
    
    def run(self): # 2. The class must have a run() function. See details below
        print("Thread {}: starting".format(self.name))
        time.sleep(2)
        print("Thread {}: finishing".format(self.name))

if __name__ == "__main__":
  for i in range(5):
      thread = ThreadFunction(i)
      thread.start() # 3. Call start() to execute the run() function
```
### How to create a threaded class:
1. The class **must inherit** *Thread*.
2. The class must have a **run()** function. Everything in this function will be executed in parallel.
3. To execute the *run()* function, you must call the **start()** function, inherited from *Thread*.

## Solving access & synchronization problems

### With Rlock:
```Python
from threading import Thread, RLock

lock = RLock()

class SyncThread(Thread):
    def __init__(self, text):
        Thread.__init__(self)
        self.text = text
    
    def run(self)
        
        # The following code is locked.
        with lock:
            print(self.text)
            with open('synch_thread.txt', 'a') as file:
                file.write(self.text)
```

In this situation, a bunch of code is locked with **with lock**. If we create multiple instances of SyncThread, only one instance at a time will have access to this bunch of code. It's your job to manage the access order. 
