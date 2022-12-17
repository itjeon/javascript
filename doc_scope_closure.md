# 스코프와 클로저

```
// 스코프와 클로저 자바스크립트 예제
function bookHotel(city){
    var availableHotel = 'None';
    for(var i=0; i < hotels.length; i++){
        var hotel = hotels[i];
        if(hotel.city === city && hotel.hasRoom){
            availableHotel = hotel.name;
            break;
        }
    }

    // 여기서 i와 hotel은 여전히 접근 가능하다.
    console.log('Checked ' + (i+1) + 'record(s)');  // Checked 2 record(s) 출력
    console.log('Last checked ' + hotel.name);
    {
        function placeOrder(){
            var totalAmount = 200;
            console.log('Order placed to ' + availableHotel);
        }
    }

    placeOrder();

    // 접근불가
    // console.log(totalAmount);

    return availableHotel;
}

var hotels = [
    {name:'Hotel A', hasRoom:false, city:'Sanya'}
    , {name:'Hotel B', hasRoom:true, city:'Sanya'}
];

console.log(bookHotel('Sanya'));

// 접근불가
// console.log(availableHotel);
```
[jsfiddle](https://jsfiddle.net/itjeon/jzuv8dnt/)


### [<-Main](https://github.com/itjeon/javascript)
