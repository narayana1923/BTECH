class Queue:
    def __init__(self):
        self.front = -1
        self.rear = -1
        self.size = 10
        self.queue = list(range(self.size))

    def enqueue(self):
        if self.rear == -1 and self.front == -1:
            self.front = self.rear = 0
        elif self.rear == self.size-1:
            print("Queue is full")
            return
        else:
            self.rear += 1
        self.queue[self.rear] = int(input("Enter value: "))

    def dequeue(self):
        if self.rear == -1 and self.front == -1:
            print("Queue is empty")
        elif self.front==self.rear:
            self.front=self.rear=-1
        else:
            self.front+=1
            print(self.queue[self.front-1],"is removed")

    def display(self):
        if self.rear == -1 and self.front == -1:
            print("Queue is empty")
        else:
            print("Queue elements are : ",end=' ')
            for i in range(self.rear,self.front-1,-1):
                print(self.queue[i],end=" ")
            print()
    
    def perform(self,option):
        if option not in range(5):
            print("Enter a valid option\n")
        else:
            if option==1:
                self.enqueue()
            elif option==2:
                self.dequeue()
            elif option==3:
                self.display()
            elif option==4:
                print("====================program ends====================")

    def start(self):
        while(True):
            print("1. Enqueue item\n"+
                  "2. dequeue item\n"+
                  "3. display item\n"+
                  "4. exit\n")
            option=int(input("Enter option: "))
            self.perform(option)
            if(option==4): break        

if __name__ == "__main__":
    q=Queue()
    print("++++++++++++++++++Implementation of Queue using arrays++++++++++++++++++")
    q.start()   
