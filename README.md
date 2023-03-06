# starvation-free-reader-writer-problem
## PROBLEM STATEMENT 
SOLUTION FOR STARVATION FREE READER WRITER PROBLEM
## PSEUDO CODE
```
Initialize

semaphore resource=1;           // for accessing resource 
semaphore mutex=1;             // for accessing the readcnt
semaphore Queue=1;           // for scheduling the requests obtained from readers and writers,so that fairness is maintained

int readcnt;                // readcnt=0,Since no reader is there at begining 

reader() {

  wait(Queue);           
  wait(mutex);                 
  readcnt++;                
  if (readcnt == 1)          //if it is the first reader
    wait(resource);            // request resource access for readers (writers blocked),since first reader 
  signal(Queue);
  signal(mutex.);                
    
<CRITICAL Section>
//reading is performed
    
  wait(mutex);                 
  readcnt--;                
  if (readcnt == 0)        //if there is no reader left
    signal(resource);          // release resource access for all
  signal(mutex);                 
}

writer() {

  wait(Queue);                 
  wait(resource);      //request for resource(block all others)           
  signal(Queue);           
    
<CRITICAL Section>
// writing is performed
    
  signal(resource);     //release the resource so that,next in the queue can get acccess to resource          
}

=>In the above code many readers can read at a time,where as writers can't.
=>No two(one reader and one writer) can enter the critical section at a time.


Explanation of statements in above code 
    wait(Queue);           // wait in queue to get access to resource(reader/writer)
    signal(Queue);         // give signal to the next (reader/writer)  in the Queue.
    wait( mutex);           // make exclusive access to particular reader to change readcnt
    signal(mutex);         // signal to change readcnt for other readers
      
```
