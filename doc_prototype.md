# 프로토타입과 상속

 User 객체 정의
```
function  User(name, interests){
	this.name = name;
	this.interests = interests;
}

User.prototype.greeting = function(){
	console.log('Hi, I\'m ' + this.name + '.');
}
```

생성자 객체를 역참조하고 있는 constructor 프로퍼티로 누가 객체를 생성하는지 확인 가능하다.
```
console.log(User.constructor === Function); // true
```

User 생성자 함수가 생성되면 프로토타입 객체를 가진다.
User 프로토타입 객체가 User생성자 함수에 의해 생성되었음을 확인
```
console.log(User.prototype.constructor === User); // true
```

User 생성자 함수로 user 객체를 생성한 이후에 user 객체는 User 프로토타입 객체를 참조하는 \_\_proto__ 프로퍼티 객체를 가진다.
 이 \_\_proto__ 참조는 프로토타입 체인에서 링크 역할을 한다.
```
var  user = new  User();
console.log(user.__proto__ === User.prototype); // true
```
User객체를 상속받아 TeamMember객체 생성
```
function  TeamMember(name, interests, tasks){
	// Function 객체에서 생성자 체인을 위해 상속받은 User 생성자 함수의 call() 메소드 호출
	// call() 메소드는 Java Class의 super()와 유사
	// 첫번째 인자는 실행 컨텍스트
	User.call(this, name, interests);
	this.tasks = tasks;
}
  
// User 객체의 프로토타입을 상속
TeamMember.prototype = Object.create(User.prototype);

// User 객체의 greeting를 재정의(Overriding). User.greeting에는 영향없음
TeamMember.prototype.greeting = function(){
	console.log('I\'m ' + this.name + '. Welcome to the team!');
};

// TeamMember 객체의 work 메소는 신규 생성. User에는 영향없음
TeamMember.prototype.work = function(){
	console.log('I\'m working on ' + this.tasks.length + ' tasks');
};
var  member = new  TeamMember('Sunny', ['Traveling'], ['Buy three tickets', 'Book a hotel.']);
member.greeting();  // I'm Sunny. Welcome to the team!
member.work();      // I'm working on 2 tasks

console.log(User.prototype === TeamMember.prototype); // false
console.log(User.prototype.constructor === TeamMember.prototype.constructor); // true

console.log(member instanceof TeamMember);  // true
console.log(member instanceof User);        // true
console.log(member instanceof Object);      // true

User.prototype.eat = function(){
    console.log('What will I have for lunch?');
};
member.eat();   // What will I have for lunch?

// 최상위 객체에 메소드 추가
// 모든 객체에 메소드가 추가되므로 매우 안 좋은 방식이다.
Object.prototype.move = function(){
    console.log('Every object can move now');
};
member.move();  // 이제 모든 객체가 move를 호출할 수 있다

var alien = {}; // 이제 모든 객체가 move를 호출할 수 있다
alien.move();   // 이제 모든 객체가 move를 호출할 수 있다
User.move();    // 이제 모든 객체가 move를 호출할 수 있다
```

프로토타입 객체는 최상위 Object객체부터의 상속을 참조하므로 조심해서 사용해야 하며 이 프로퍼티를 잘 못 변경하면 상속이 깨진다.
```
console.log(member.__proto__ === TeamMember.prototype);             // true
console.log(TeamMember.prototype.__proto__ === User.prototype);     // true
console.log(User.prototype.__proto__ === Object.prototype);         // true

User.prototype.__proto__ = null;
// member.move();  // Uncaught TypeError: member.move is not a function
console.log(member instanceof Object);  // false
```
[jsfiddle](https://jsfiddle.net/itjeon/n82hpqf1/)


### [<-Main](https://github.com/itjeon/javascript)
