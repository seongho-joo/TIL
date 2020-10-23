# Property

1. 프로퍼티의 종류
   * 인스턴스 저장 프로퍼티
   * 타입 저장 프로퍼티
   * 인스턴스 연산 프로퍼티
   * 타입 연산 프로퍼티
   * 지연 저장 프로퍼티
  
2. 정의와 사용
   * 연산 프로퍼티는 `var`로만 선언 가능
   * 읽기는 `get` 블럭, 쓰기는 `set` 블럭 사용
   * `set` 블럭에서 매개변수를 지정하지 않으면 암시적 매개변수로 **newValue**를 사용할 수 있음  
       
         struct Money {
             var currencyRate: Double = 1100
             var dollar: Double = 0
             // 연산 프로퍼티
             var won: Double {
                 get { // 읽기
                     return dollar * currencyRate
                 }
                 set { // 쓰기
                     dollar = newValue / currencyRate
                 }
             }
         }

         var moneyInMyPocket = Money()

         moneyInMyPocket.won = 11000

         print(moneyInMyPocket.dollar)
         // 10

         print(moneyInMyPocket.won)
         // 11000

         moneyInMyPocket.dollar = 10

         print(moneyInMyPocket.won)
         // 11000

3. 프로퍼티 감시자
    * 프로퍼티 감시자를 사용하면 프로퍼티의 값이 변경될 때 원하는 동작을 수행할 수 있음.
    * 값이 변경되기 직전에 `willSet`블럭이, 값이 변경된 직후에 `didSet`블럭이 호출됨.
    * 변경되려는 값이 기존 값과 똑같더라도 프로퍼티 감시자는 항상 동작
    * `willSet` 블럭에서는 암시적 매개변수 **newValue**를 사용하고 `didSet` 블럭에서는 **oldValue** 사용
    * 프로퍼티 감시자는 연산 프로퍼티에는 사용할 수 없음.
    * 프로퍼티 감시자는 함수, 메서드, 클로저, 타입 등의 지역/전역 변수에 모두 사용 가능
              
          var a: Int = 100 {
              wilSet {
                  // 현재 값에서 새로운 값으로 변경되기 전에 실행
                  print("\(a) -> \(newValue) 변경 예정")
              }
              didSet {
                  // 값이 변경된 후 실행
                  print("\(oldValue) -> \(a) 변경 됨")
              }
          }

          a = 200
          // 100 -> 200 변경 예정
          // 100 -> 200 변경 됨