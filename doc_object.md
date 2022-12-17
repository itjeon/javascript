### 객체

###### 객체를 생성하는 방식

1. <a href="https://jsfiddle.net/itjeon/gw6c104q/1" target="_blank">Object() 생성자</a> : 객체 래퍼(Wrapper)를 생성, 비권장, 객체리터럴 방식이 낫다
  
  ```
  // new를 활용한 Object 생성자 호출
  var user = new Object();
  user.name = 'Sunny';
  user.interests = ['Travbeling', 'Swimming'];
  user.greeting = function(){
      console.log('Hi, I\'m ' + this.name + '.');
  };
  user.greeting();    // Hi, I'm Sunny.
  ```
  
2. <a href="https://jsfiddle.net/itjeon/gw6c104q/6/" target="_blank">객체리터럴</a>
  
  ```
  // 객체 리터럴을 활용한 user 생성
  var user = {
      name: 'Sunny',
      interests: ['Traveling', 'Swimming'],
      greeting: function(){
          console.log('Hi, I\'m ' + this.name + '.');
      },
      // ES5부터 Getter/Setter 지원
      get role(){
          return 'Engineer';
      }
  }
                              
  user.greeting();            // Hi, I'm Sunny.
  console.log(user.role);     // Engineer
  user.role = 'Manager';      // Setter 접근자가 없으므로 값이 변경되지 않는다.
  console.log(user.role);     // Engineer
  ```
  
3. <a href="https://jsfiddle.net/itjeon/gw6c104q/7/" target="_blank">생성자 함수</a>
  
  ```
  // 생성자 함수 생성
  function User(name, interests){
      this.name = name;
      this.interests = interests;
      this.greeting = function(){
          console.log('Hi, I\'m ' + this.name + '.');
      }
  }
  
  // user객체를 생성하는데 new를 활용해 생성자 함수 호출
  var user = new User('Sunny', ['Traveling', 'Swimming']);
  user.greeting();            // Hi, I'm Sunny.
  ```
  
4. <a href="https://jsfiddle.net/itjeon/gw6c104q/8/" target="_blank">Object.create()</a>
  
  ```
  // 위에서 생성한 User 생성자 함수의 프로토타입과 Object.create() 메소드 활용
  var user = Object.create(User.prototype, {
      name : {value: 'Sunny'},
      interests: {value: ['Traveling', 'Swimming']},
  });
  user.greeting();            // user.greeting is not a function
  
  User.prototype.greeting = function(){
      console.log('Hi, I\'m ' + this.name + '.');
  }
  user.greeting();            // Hi, I'm Sunny.
  ```
  
5. <a href="https://jsfiddle.net/itjeon/gw6c104q/10" target="_blank">생성함수</a>
  
  ```
  // 객체를 반환하는 생성 함수 사용
  function createUser(name, interests){
      var user = {};
      user.name = name;
      user.interests = interests;
      user.greeting = function(){
          console.log('Hi, I\'m ' + this.name + '.');
      };
      return user;
  }
   
  // 매개변수를 이용해 생성 함수 호출
  var user = createUser('Sunny', ['Traveling', 'Swimming']);
  user.greeting();            // Hi, I'm Sunny.
  ```
  
6. <a href="https://jsfiddle.net/itjeon/gw6c104q/11/" target="_blank">ES6의 클래스 선언</a>
  ```
  // User 클래스 생성
  class User{
  	// User 생성자 함수와 상응
  	constructor(name, interests){
  		this.name = name;
  		this.interests = interests;
  	}
  	
  	// User.prototype.greting과 같다.
  	greeting(){
  		console.log('Hi, I\'m ' + this.name + '.');
  	}
  }
  
  let user = new User('Sunny', ['Traveling', 'Swimming']);
  user.greeting();            // Hi, I'm Sunny.
  ```
7. <a href="https://jsfiddle.net/itjeon/gw6c104q/12/" target="_blank">ES6의 클래스 표현식</a>
  ```
  let User = class {
  	// User 생성자 함수와 상응
  	constructor(name, interests){
  		this.name = name;
  		this.interests = interests;
  	}
  	
  	// User.prototype.greting과 같다.
  	greeting(){
  		console.log('Hi, I\'m ' + this.name + '.');
  	}
  }
  
  let user = new User('Sunny', ['Traveling', 'Swimming']);
  user.greeting();            // Hi, I'm Sunny.
  ```

### [<-Main](https://github.com/itjeon/javascript)
