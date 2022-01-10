# 연결리스트

* 노드

  자료구조에 데이터를 담거나 표현하는 기초적인 단위

  특정 값 or 포인터

  

- **연결 리스트 특징**

- 1. 크기를 미리 정하지 않고도 동적 할당이 가능
  2. 삽입과 삭제 연산에서 오버헤드가 배열보다 적음
  3. 특정 인덱스로 접근이 불가능하므로 데이터를 검색하려면 순차적으로 첫 노드부터 끝까지 방문을 해야함.



* **연결리스트 종류**

  * **단일 연결 리스트**

    첫 노드를 가리키는 head  변수를 가지고 있음

    각각의 노드는 자신의 다음 노드를 가리키며, 가리킬 대상이 없으면 null을 가리킴
    

    ```java
    //단일리스트
    public class SinglyLinkedList {
    	private Node head;
    	
    	public SinglyLinkedList() { //생성자
    		this.head = null;
    	}
    	
    	public SinglyLinkedList(int value) {
    		this.head = new Node(value, null);
    	}
    	
    	class Node{  //Node 클래스
    		private int value;  ///값
    		private Node next;  //포인터, 단일리스트기 떄문에 포인트는 하나만 
    	
    		Node(int value, Node next){
    			this.value = value;
    			this.next = next;
    		}
    		
    		public int getValue() {
    			return this.value;
    		}
    	}
    	
    	public Node getHead() {
    		return this.head;
    	}
    	
    	public void append(int value) { //연결리스트의 마지막 위치에 노드를 삽입
    		if(this.head == null) { //빈 연결리스트일 때
    			this.head = new Node(value, null); //새 노드를 생성 후 head에 할당
    			return;
    		}
    		
    		Node pointer = this.head;
    		while(pointer.next != null) { //pointer 변수가 null이 아닐 때까지
    			pointer = pointer.next; //포인터는 다음 포인터로
    		} //while문을 빠져나오면 pointer = 마지막 노드
    		
    		pointer.next = new Node(value, null); //인자로 받은 value값으로 새 노드를 생성, 마지막 노드의 포인터는 새노드를 가리키도록 함
      	}
    	
    	
    	public void delete(int value) {//노드 삭제
    		Node pointer = this.head;
    		
    		if(pointer.getValue() == value) { //첫 노드의 값이 인자 값과 동일할 때
    			Node removeNode = this.head;
    			this.head = this.head.next;
    			
    			removeNode = null;
    			return;
    		}
    		
    		Node temp = pointer;
    		
    		while(pointer != null && pointer.getValue() != value) { //null이 아니면서, 인자 값과 달라질 때까지
    			temp = pointer;
    			pointer = pointer.next;
    		}
    		
    		if(pointer.next == null) {
    			temp.next = null;
    		}else {
    			temp.next = pointer.next;
    		}
    		pointer = null;
    	}
    	
    	public void printAll() { //모든 노드 출력
    		Node pointer = this.head;
    		
    		StringBuilder builder = new StringBuilder();
    		while(pointer.next != null) { //pointer 변수가 null이 아닐때까지
    			builder.append(pointer.getValue());
    			builder.append(" -> ");
    			pointer = pointer.next;
    		} 
    		
    		builder.append(pointer.getValue());	
    		System.out.println(builder.toString());
    		
    	}
    }
    
    ```

    

    

  * **이중 연결 리스트**

    자신과 인접해 있는 노드들을 모두 가리킴

    ```JAVA
    //이중리스트  - 두개의 포인터 사용
    public class DoubleLinkedList {
    	private Node head;
    	
    	public DoubleLinkedList() { //생성자
    		this.head = null;
    	}
    	
    	public DoubleLinkedList(int value, Node ehead) {
    		this.head = new Node(value, head, null);
    	}
    	
    	class Node{  //Node 클래스
    		private int value;  //값
    		private Node prev;  //이전 포인터
    		private Node next;  //다음 포인터
    	
    		Node(int value){
    			this.value = value;
    			this.prev = null;
    			this.next = null;
    		}
    		
    		Node(int value, Node prev, Node next){
    			this.value = value;
    			this.prev = prev;
    			this.next = next;
    		}
    		
    		public int getValue() {
    			return this.value;
    		}
    	}
    	
    	public Node getHead() {
    		return this.head;
    	}
    	
    	public void append(int value) { //노드를 삽입
    		if(this.head == null) { //빈 리스트일 때
    			this.head = new Node(value); //새 노드를 생성 후 head에 할당
    			return;
    		}
    		
    		Node pointer = this.head;
    		while(pointer.next != null) { //pointer 변수가 null이 아닐 때까지
    			pointer = pointer.next; //포인터는 다음 포인터로
    		} //while문을 빠져나오면 pointer = 마지막 노드
    		
    		Node newNode = new Node(value); 
    		newNode.prev = pointer; //새 노드의 prev 포인터를 pointer 변수로 가리킴 
    		pointer.next = newNode; //pointer 변수의 다음은 새 노드
      	}
    	
    	public void printPreNode(int value) { //인자 값으로 노드의 값 알아냄
    		if(this.head == null) {
    			System.out.println("이중 연결 리스트가 비어 있습니다.");
    			return;
    		}
    		
    		if(this.head.getValue() == value) {
    			System.out.println(String.format("노드 %s 의 앞 노드는 존재하지 않습니다.",value));
    			return;
    		}
    		
    		Node pointer = this.head;  //pointer 변수는 head를 가리킴
    		while(pointer != null && pointer.getValue() != value) {
    			pointer = pointer.next;
    		}
    		
    		
    		if(pointer == null) {
    			System.out.println(String.format("노드 %s 은 존재하지 않습니다.", value));
    		} else {
    			System.out.println(String.format("노드 %s 의 앞 노드의 값은 %s 입니다.", value, pointer.prev.getValue()));
    			return;
    		}
    	}
    	
    	
    	public void delete(int value) {//노드 삭제
    		Node pointer = this.head;
    		
    		if(pointer.getValue() == value) { //첫 노드의 값이 인자 값과 동일할 때
    			Node removeNode = this.head;
    			this.head = this.head.next;
    			
    			removeNode = null;
    			return;
    		}
    		
    		Node prevNode = pointer;  // 삭제된 노드와 인접한 노드를 연결시키기 위해 사용
    		while(pointer != null && pointer.getValue() != value) { //null이 아니면서, 인자 값과 달라질 때까지
    			prevNode = pointer;
    			pointer = pointer.next;
    		}
    		
    		Node temp = pointer.next;
    		if(temp == null) {
    			prevNode.next = null;
    		}else {
    			temp.prev = prevNode; //재할당
    			prevNode.next = pointer.next;
    		}
    		pointer = null;
    	}
    	
    	public void printAll() { //모든 노드 출력
    		Node pointer = this.head;
    		
    		StringBuilder builder = new StringBuilder();
    		while(pointer.next != null) { //pointer 변수가 null이 아닐때까지
    			builder.append(pointer.getValue());
    			builder.append(" -> ");
    			pointer = pointer.next;
    		} 
    		
    		builder.append(pointer.getValue());	
    		System.out.println(builder.toString());
    		
    	}
    }
    
    ```

    

    

  * **원형 단일 연결 리스트**

    첫 노드를 가리키는 head 변수와 마지막 노드를 가리키는 tail변수를 가지고 있음

    ```java
    //원형 리스트  -  head와 tail
    //원형 연결 리스트는 마지막 노드를 기억하고 있으므로 마지막 노드를 구하기 위해 노드를 순회하지 않아도 됨. tail을 이용하여 삽입연산을 수행
    public class CircularLinkedList {
    	private Node head;
    	private Node tail;
    	
    	public CircularLinkedList() { //생성자
    		this.head = null;
    		this.tail = null;
    	}
    	
    	class Node{  //Node 클래스
    		private int value;  //값
    		private Node next;  //다음 포인터
    	
    		Node(int value){
    			this.value = value;
    			this.next = null;
    		}
    		
    		public int getValue() {
    			return this.value;
    		}
    	}
    	
    	public Node getHead() {
    		return this.head;
    	}
    	
    	public void append(int value) { //원형 단일 연결 리스트 끝에 노드 추가
    		if(this.head == null && this.tail == null) {
    			Node node = new Node(value);
    			this.head = node;
    			this.tail = node;
    			return;
    		}
    		
    		Node pointer = this.tail;
    		
    	    pointer.next = new Node(value);  //마지막 위치에 새 노드 삽입	    
    	    this.tail = pointer.next; //tail은 새로 삽입한 노드를 재할당
    	    
    	    //tail의 next 포인트를 head로 연결하여 원형 연결 리스트 조건 만족시킴
    	    this.tail.next = head;
    	}
    	
    	public void delete(int value) {//노드 삭제
    		Node pointer = this.head;
    		
    		if(pointer.getValue() == value) { //첫 노드의 값이 인자 값과 동일할 때
    			Node removeNode = this.head;
    			this.head = this.head.next;
    			
    			removeNode = null;
    			return;
    		}
    		
    		//포인터가 tail이 아니며 값이 다를 때까지 
    		Node temp = null;
    		
    		while(pointer.next != this.tail && pointer.getValue() != value) {
    			temp = pointer;
    			pointer = pointer.next;
    		}
    		
    		if(pointer.next.getValue() == value) { //삭제할 노드가 tail일 때
    			this.tail = pointer; //앞 노드를 tail로 재할당
    			this.tail.next = pointer.next; //포인터의 next를 head로 연결
    		}else { ///삭제되는 노드가 head와 tail의 중간 노드일 때
    			temp.next = pointer.next; 
    		}
    		pointer = null;
    	}
    	
    	public void printAll() { //모든 노드 출력
    		Node pointer = this.head;
    		
    		StringBuilder builder = new StringBuilder();
    		while(pointer != this.tail) { //pointer 변수가 null이 아닐때까지
    			builder.append(pointer.getValue());
    			builder.append(" -> ");
    			pointer = pointer.next;
    		} 
    		
    		builder.append(pointer.getValue());	
    		builder.append("(tail) -> ");
    		
    		builder.append(this.head.getValue());	
    		builder.append("(head)");
    		
    		System.out.println(builder.toString());
    		
    	}
    }
    ```

    