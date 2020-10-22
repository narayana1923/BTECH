class Node:
    def __init__(self):
        self.data = 0
        self.next = None

class Queue:
    def __init__(self):
        self.front = None
        self.rear=None

    def enqueue(self):
        node = Node()
        if node is None:
            print("Memory is full !!!\n")
            return
        node.data = int(input("Enter value to be inserted : "))
        if self.front is None:
            self.front = node
            self.rear = node
        else:
            self.rear.next=node
            self.rear=node
        print("Value added\n")

    def dequeue(self):
        if(self.front is None):
            print("Queue is empty\n")
        else:
            val = self.front.data
            self.front = self.front.next
            print(val, " is removed from the Queue\n")

    def display(self):
        if(self.front is None):
            print("Queue is empty\n")
            return
        print("\nStack elements are: \n")
        i = 0
        ptr = self.front
        while(ptr):
            print("Element - ",i+1," : ",ptr.data,"\n")
            ptr = ptr.next
            i += 1
        print()

    def perform(self,option):
        if(option not in range(1, 5)):
                print("Enter a valid option\n")
        else:
            if(option == 1):
                self.enqueue()
            elif(option == 2):
                self.dequeue()
            elif option==3:
                self.display()
            elif option == 4:
                print("==========Program ends=============")
    
    def start(self):
        while(True):
            print("1.enqueue an Element on to Stack\n"+
                    "2.dequeue an Element from Stack\n"+
                    "3.Display the elements of a Stack\n"+
                    "4.Exit\n\n")
            option = int(input("Enter your option : "))
            self.perform(option)
            if(option == 4): break

if __name__ == "__main__":
    print("~~~~~~~~~~~~~~~~~~~~~~~~~~~~Implementation Of Stack with linked list~~~~~~~~~~~~~~~~~~~~~~~~~~~~\n")
    s=Queue()
    s.start()
