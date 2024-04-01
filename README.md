# WGU D286 Java Fundamentals

## 13.1 LAB: Caffeine levels
	import java.util.Scanner; 

	public class LabProgram {
	   public static void main(String[] args) {
		  Scanner scnr = new Scanner(System.in); 
		  double caffeineMg; // "double" supports floating-point like 75.5, versus int for integers like 75. 
		  
		  caffeineMg = scnr.nextDouble(); 
		  double caffeineLvl = caffeineMg / 2;
		  System.out.printf("After 6 hours: %.2f mg\n", caffeineLvl);
		  caffeineLvl = caffeineLvl / 2;
		  System.out.printf("After 12 hours: %.2f mg\n", caffeineLvl);
		  caffeineLvl = caffeineLvl / 4;
		  System.out.printf("After 24 hours: %.2f mg\n", caffeineLvl);
	   }
	}

## 13.2 LAB: Driving costs
	import java.util.Scanner;

	public class LabProgram {
	   public static void main(String[] args) {
		  Scanner scnr = new Scanner (System.in);
		  double gasMilage = scnr.nextDouble();
		  double gasCost = scnr.nextDouble();
		  double costx20 = (gasCost / gasMilage)  * 20;
		  double costx75 = (gasCost / gasMilage)  * 75;
		  double costx500 = (gasCost / gasMilage)  * 500;
		  System.out.printf("%.2f %.2f %.2f\n", costx20, costx75, costx500);
	   }
	}

## 13.3 LAB: Phone number breakdown
	import java.util.Scanner;

	public class LabProgram {
	   public static void main(String[] args) {
		  Scanner scnr = new Scanner(System.in);
		  long phoneNumber;
		  phoneNumber = scnr.nextLong();
		  long line = phoneNumber  % 10000;
		  long prefix = (phoneNumber  / 10000) % 1000;
		  long area = (phoneNumber / 10000000 );
		  //System.out.println ("("+area+") "+prefix+"-" + line);
		  System.out.printf ("(%d) %d-%d\n",area,prefix,line);
	   }
	}


## 13.4.1 LAb Musical note frequencies.
	import java.util.Scanner;

	public class LabProgram {
	   public static void main(String[] args) {
		  Scanner scnr = new Scanner(System.in);
		  double f = scnr.nextDouble();
		  double p = 1.0/12.0;
		  double r = Math.pow (2,p);
		  double n1,n2,n3,n4;
		  n1 = f * Math.pow(r,1);
		  n2 = f * Math.pow(r,2);
		  n3 = f * Math.pow(r,3);
		  n4 = f * Math.pow(r,4);      
		  System.out.printf("%.2f %.2f %.2f %.2f %.2f\n",f,n1,n2,n3,n4);
	   }
	}
## 19.1 LAB: List count
#### CustomLinkedList.java
	public class CustomLinkedList {
	   
	   // TODO: Return number of nodes in list
	   public static int getCount(IntNode headObj) {
		  IntNode node = headObj.getNext();
		  int t = 0;
		  while (node!=null){
			 t++;
			 //System.out.print (node.getNodeData());
			 node = node.getNext();
		  }
		  return t;
	   }
	   
	   public static void main(String[] args) {
		  IntNode headObj; 
		  IntNode currObj;
		  IntNode lastObj;
		  int i; 
		  int count;
		  
		  // Create head node
		  headObj = new IntNode(-1); 
		  lastObj = headObj;
		  
		  // Add nodes to the list
		  for (i = 0; i < 20; ++i) { 
			 currObj = new IntNode(i);         
			 lastObj.insertAfter(currObj); 
			 lastObj = currObj;
		  }
		  
		  count = getCount(headObj);
		  System.out.println(count);
	   }
	}
	
#### intNode.java
	public class IntNode {
	   private int dataVal;         // Node data
	   private IntNode nextNodePtr; // Reference to the next node

	   // Default constructor
	   public IntNode() {
		  dataVal = 0;
		  nextNodePtr = null;
	   }

	   // Constructor
	   public IntNode(int dataInit) {
		  this.dataVal = dataInit;
		  this.nextNodePtr = null;
	   }

	   // Constructor
	   public IntNode(int dataInit, IntNode nextLoc) {
		  this.dataVal = dataInit;
		  this.nextNodePtr = nextLoc;
	   }

	   /* Insert node after this node.
		Before: this -- next
		After:  this -- node -- next
		*/
	   public void insertAfter(IntNode nodeLoc) {
		  IntNode tmpNext;

		  tmpNext = this.nextNodePtr;
		  this.nextNodePtr = nodeLoc;
		  nodeLoc.nextNodePtr = tmpNext;
	   }

	   // Get location pointed by nextNodePtr
	   public IntNode getNext() {
		  return this.nextNodePtr;
	   }

	   // Get node value
	   public int getNodeData() {
		  return this.dataVal;
	   }
	   
	   // Print node value
	   public void printNodeData() {
		  System.out.println(this.dataVal);
	   }
	}

## 19.2 LAB: Index of list item
	public class CustomLinkedList {
	   
	   // TODO: Return index of target item
	   public static int indexOf(IntNode headObj, int target) {
		  boolean found = true;
		  IntNode node = headObj.getNext();
		  int index = 0;
				
		  while (true){
			 if (node==null) return -1;
			 if (node.getNodeData()==target){
				return index;
			 }
			 index++;
			 node=node.getNext();
		  }      
	   }
	   
	   public static void main(String[] args) {
		  IntNode headObj; 
		  IntNode currObj;
		  IntNode lastObj;
		  int i; 
		  int index;
		  
		  // Create head node
		  headObj = new IntNode(-1); 
		  lastObj = headObj;
		  
		  // Add nodes to the list
		  for (i = 0; i < 20; ++i) { 
			 currObj = new IntNode(i);         
			 lastObj.insertAfter(currObj); 
			 lastObj = currObj;
		  }    
		  
		  index = indexOf(headObj, 15);
		  System.out.println(index);
	   }
	}
	

## 19.3.1: LAB: Is list sorted

	public class CustomLinkedList {
	   
	   // TODO: Return true if list items are in ascending order
	   public static boolean isSorted(IntNode headObj) {
		  boolean sorted = false;
		  IntNode previous, current;
		  IntNode node = headObj.getNext(); 
		  if (node==null) return true;  //List is empty, return true
		  previous = node;
		  current = node.getNext();
		  if (current == null) return true; //List has only one element, return true
		  while (true){
			 if (previous.getNodeData() > current.getNodeData() ) return false;
			 previous = current;
			 current = current.getNext();
			 if (current==null) return true;         
		  }
		  
	   }
	   
	   public static void main(String[] args) {
		  IntNode headObj; 
		  IntNode currObj;
		  IntNode lastObj;
		  int i; 
		  boolean result;
		  
		  // Create head node
		  headObj = new IntNode(-1); 
		  lastObj = headObj;
		  
		  // Add nodes to the list
		  for (i = 0; i < 20; ++i) { 
			 currObj = new IntNode(i);         
			 lastObj.insertAfter(currObj); 
			 lastObj = currObj;
		  }
		  
		  result = isSorted(headObj);
		  System.out.println(result);
	   }
	}

## 19.4 1: LAB: Warm up: Contacts

### ContactList.java
	import java.util.Scanner;

	public class ContactList {
      
      
   public static void main(String[] args) {  
      ContactNode heap = new ContactNode();
	      Scanner scnr = new Scanner(System.in);
	      /* Type your code here. */
	      ContactNode contact1 = new ContactNode (scnr.nextLine(), scnr.nextLine());
	      heap.insertAfter (contact1);
	      ContactNode contact2 = new ContactNode (scnr.nextLine(), scnr.nextLine());
	      contact1.insertAfter(contact2);
	      ContactNode contact3 =  new ContactNode (scnr.nextLine(), scnr.nextLine());
	      contact2.insertAfter(contact3);
	      
	      System.out.println ("Person 1: " + contact1.getName() + ", " + contact1.getPhoneNumber());
	      System.out.println ("Person 2: " + contact2.getName() + ", " + contact2.getPhoneNumber());
	      System.out.println ("Person 3: " + contact3.getName() + ", " + contact3.getPhoneNumber());
	      System.out.println("\nCONTACT LIST");
	      ContactNode node = heap.getNext();      
	      while (node!=null){
	         node.printContactNode();
	         System.out.println();
	         node = node.getNext();
	      }
	   }
	}

###  ContactNode.java

	public class ContactNode {
	   private String contactName;
	   private String contactPhoneNumber;
	   private ContactNode nextNodePtr;

	   public ContactNode(){
		  this.contactName="";
		  this.contactPhoneNumber="";
		  this.nextNodePtr=null;
	   }
	   
	   public ContactNode (String name, String phone){
		  this.contactName = name;
		  this.contactPhoneNumber = phone;  
	   }
	   
	   public String getName(){
		  return this.contactName;
	   }
	   
	   public String getPhoneNumber(){
		  return this.contactPhoneNumber;
	   }

	   public void insertAfter(ContactNode node){
		  this.nextNodePtr = node;
	   }
	   
	   public ContactNode getNext(){
		  return this.nextNodePtr;
	   }
	   public void printContactNode(){
		  System.out.println ("Name: "+ this.contactName);
		  System.out.println ("Phone number: " + this.contactPhoneNumber);      
	   }   
	}

## 20.1 Practice Lab 1
	public class LabProgram {
	   public static void main(String[] args) {
		  System.out.println("H   H");
		  System.out.println("H   H");
		  System.out.println("HHHHH");
		  System.out.println("H   H");
		  System.out.println("H   H");
	   }
	}
	
	

## 20.2.1: Practice Lab 2
	import java.util.Scanner;

	public class LabProgram {
	   public static void main(String[] args) {
		  Scanner scnr = new Scanner(System.in); 
		  /* Type your code here. */
		  int starting_num = scnr.nextInt();
		  int multiplier = scnr.nextInt();
		  int r = starting_num * multiplier;
		  int r2 = r * multiplier;
		  int r3 = r2 *  multiplier;
		  System.out.printf ("%d %d %d\n",r,r2,r3);
	   }
	}

## 20.3 Practice Lab 3
	import java.util.Scanner;

	public class LabProgram {
		public static void main(String[] args) {
			Scanner scnr = new Scanner(System.in);
			int tableSize=10, guests, tablesFilled;
		  guests = scnr.nextInt();
		  tablesFilled = guests / tableSize;
		  System.out.printf ("Tables filled: %d\n",tablesFilled);      
	   }
	}

## 20.4 Practice Lab 4
	import java.util.Scanner;

	public class LabProgram {
	   public static void main(String[] args) {
		  Scanner scnr = new Scanner(System.in);        
		  String name, age, salary;
		  name = scnr.nextLine();
		  age = scnr.nextLine();
		  salary = scnr.nextLine();      
		  System.out.printf("%s is %s and makes $%s.\n",name,age,salary);      
	   }
	}
	

## 20.5.1: Practice Lab 5
	import java.util.Scanner;

	public class LabProgram {
	   public static void main(String[] args) {
		  Scanner scnr = new Scanner(System.in);         
		  int n1 = scnr.nextInt();
		  int n2 = scnr.nextInt();
		  int n3 = scnr.nextInt();
		  if ((n1<0) || (n2<0) || (n3<0)){
			 System.out.println ("Invalid input!");
		  }else{
			 int num = (n1*100 + n2*10 +n3);
			 int d =  num % 3;          
			 String msg = (d==0) ? "is" : "is not";
			 System.out.printf ("%d%d%d %s divisible by 3!\n",n1,n2,n3,msg);
		  }      
	   }
	}

## 20.6 Practice Lab 6
	public class LabProgram {
	   public static void main(String[] args) {
		  Scanner scnr = new Scanner(System.in);       
		  String fullName = scnr.nextLine();
		  String[] words =fullName.split(" ");
		  String first,last="",middle="";
		  first = words[0];
		  if (words.length==3) {
			 middle = words[1];
			 middle = " "+middle.charAt(0)+".";
			 last = words[2];
		  }
		  if (words.length==2) {
			 last = words[1];
		  }
		  System.out.println (last.charAt(0)+"., "+first+middle);
	   }
}

## 20.7 Practice Lab 7
	import java.util.Scanner; 

	public class LabProgram {
	   public static void main(String[] args) {
		  Scanner scnr = new Scanner(System.in);      
		  int n = scnr.nextInt();
		  int small = n;
		  int sum = 0;
		  while (n>=0) {
			 sum+=n;
			 if (n<small) small=n;
			 n = scnr.nextInt();
		  }
		  System.out.printf ("Smallest: %d\nSum: %d\n", small, sum);      
	   }
	}

## 20.8 Practice Lab 8
	import java.util.Scanner;

	public class LabProgram {
	   public static void main(String[] args) {
		  Scanner scnr = new Scanner(System.in);
		  double[] nums = new double[3];
		  double n;
		  double total = 0;
		  for (int i=0;i<3;i++){
			 n = scnr.nextDouble();
			 total+=n;
			 nums[i]=n;
		  }
		  double avg = total / 3;
		  System.out.println ("Array items: "+nums[0]+", "+ nums[1]+", "+nums[2]);
		  System.out.println ("Average: " + avg);
	   }
	}
	
## 20.9 Practice Lab 9
	import java.util.Scanner;
	import java.util.Random;

	public class LabProgram {   
	   
	   boolean showResults (Random r) {
		  int rn = r.nextInt(2);
		  if (rn==1) {
			 return true;
		  }
		  return false;       
	   }
	   
	   public static void main(String[] args) {
		  Scanner scnr = new Scanner(System.in);
		  Random rand = new Random(2); // Seed used in develop mode
		  LabProgram app = new LabProgram();
		  int l = scnr.nextInt();
		  for (int i=0; i<l;i++){
			 System.out.println(app.showResults (rand));
		  }
		  
	   }
	}
## 20.10 Practice Lab 10
	import java.util.Scanner;

	public class CustomerAge {
	   public static void main(String[] args) {
		  Scanner scnr = new Scanner(System.in);
		  
		  Customer customer1 = new Customer();
		  Customer customer2 = new Customer();
		  
		  // TODO: Declare name and age variables (string, and int)
		  String name;
		  int age;
		  
		  // TODO: Read name and age input for customer 1
		  name = scnr.next();
		  age = scnr.nextInt();
		  
		  // TODO: Set customer 1 name and age fields using mutator methods (setName() and setAge())      
		  customer1.setName (name);
		  customer1.setAge (age);      

		  // TODO: Read name and age input for customer 2
		  name = scnr.next();
		  age = scnr.nextInt();
		  
		  // TODO: Set customer 2 name and age fields using mutator methods (setName() and setAge())
		  customer2.setName (name);
		  customer2.setAge (age);      
		  
		  System.out.println("Customer that is older:");
		  
		  /// TODO: Determine older customer (use getAge())
		  //       and output older customer's info (use printInfo())
		  if (customer1.getAge()>customer2.getAge() ) {
			 customer1.printInfo();
		  } else {
			 customer2.printInfo();
		  }
	   }
	}
## 20.11 Practice Lab 11. Debt ratio

public class Debt {
    // TODO: Declare private field - debtRatio  
   private double debtRatio;
      
   // TODO: Define public method - calculateDR()
     public void calculateDR (double totalDebt, double totalAssets){
        this.debtRatio = totalDebt / totalAssets;
     }
   
   // TODO: Define public method - getDR()
   public double getDR (){
      return debtRatio;
   }   
}


## 20.12.1: Practice Lab 12
	public class Pet {
		// TODO: Declare private fields 
		private String name;
		private String type;
		private int age;
		
		// TODO: Define no-arg constructor 
		public Pet() {
		   this.name ="unknown";
		   this.type="unknown";
		   this.age=0;
		}
	   
	   public Pet(String name, String type, int age) {
		   this.name = name;
		   this.type = type;
		   this.age = age;
		}
	   
	   // TODO: Define getter (accessor) methods and setter (mutator) methods
	  public String getName (){
		 return this.name;
	  }
	   public String getType (){
		 return this.type;
	  }
	  public int getAge (){
		 return this.age;
	  }
	  
	  //setters
	  public void setName (String name){
		 this.name = name;
	  }
	  
	  public void setType (String type){
		 this.type = type;
	  }
	  
	  public void setAge (int age){
		 this.age = age;
	  }
	   
	}
## 20.13 Practice Lab 13- Derived Classes
	public class RubberDuck extends Duck {
		 public String getBehavior() {
			return "squeaks";
		   } 
	}
	
public class MallardDuck extends Duck{
		public String getBehavior() {
			return "flies";
		}     
	}	
	
## 20.14 Practice Lab 14 Classes
import java.util.ArrayList;

public class Customer {
   private int id;
   private String name;
   
   //TODO: Create a Grocery ArrayList
   private ArrayList<Grocery> groceries = new ArrayList<>();
   
   //TODO: Define getGroceryList() method that returns Grocery ArrayList  
   public ArrayList<Grocery> getGroceryList(){
      return groceries;
   }
    
   //TODO: Define addGrocery(Grocery grocery) that adds a Grocery object to Grocery ArrayList via the grocery parameter
   public void addGrocery(Grocery item){
      groceries.add (item);
   }
   
   public int getId() {
      return id;
   }

   public void setId(int id) {
      this.id = id;
   }

   public String getName() {
      return name;
   }

   public void setName(String name) {
      this.name = name;
   }
   
   
   
}








