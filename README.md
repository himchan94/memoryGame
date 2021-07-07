# Memory-Game
Simple Game made with HTML, CSS, JS
------
### overview
![image](https://user-images.githubusercontent.com/71649055/124699335-94503300-df25-11eb-9460-fbffbb748e4b.png)

#### 1) 랜덤 이미지 배열 생성
sort와 Math.randoe()을 이용해서 랜덤한 숫자값을 생성한다.
```
  cardArray.sort(() => {
    return 0.5 - Math.random();
  });
```
```
  function createBoard() {
    for (let i = 0; i < cardArray.length; i++) {
      const card = document.createElement("img");  // img 태그 생성
      card.setAttribute("src", "src/images/blank.png"); // 이미지 src 값 추가
      card.setAttribute("data-id", i); // 카드 ID 생성
      card.addEventListener("click", flipCard); // 카드 클릭 시 발생하는 이벤트 추가
      grid.appendChild(card); //   const grid = document.querySelector(".grid"); 그리드 하위로 추가

    }
  }
```

### 2) 카드 클릭 이벤트 함수
```
  function flipCard() {
    let cardId = this.getAttribute("data-id"); // 카드의 id 값을 가져옴
    cardsChosen.push(cardArray[cardId].name);
    cardChosenIds.push(cardId);
    this.setAttribute("src", cardArray[cardId].img);
    if (cardsChosen.length === 2) { // 배열에 카드 2개가 들어온다면
      setTimeout(checkForMatch, 500); // 배열 내의 2카드가 서로 같은지 헉인힌다.
    }
    console.log(cardChosenIds);
  }
```

### 3) 카드 확인 이벤트 함수
```
  function checkForMatch() {
    const cards = document.querySelectorAll("img");
    const optionOneId = cardChosenIds[0]; // 배열로 들어온 카드 1
    const optionTwoId = cardChosenIds[1]; // 배열로 들어온 카드 2

    if (optionOneId == optionTwoId) { // 같은 카드를 두 번 눌렀을 때
      alert("You have clicked same img");
      cards[optionOneId].setAttribute("src", "src/images/blank.png");
      cards[optionTwoId].setAttribute("src", "src/images/blank.png");
    } else if (cardsChosen[0] === cardsChosen[1]) { // 배열 내 다를 떄
      alert("You have found match!");
      cards[optionOneId].setAttribute("src", "src/images/white.png");
      cards[optionTwoId].setAttribute("src", "src/images/white.png");
      cards[optionOneId].removeEventListener("click", flipCard);
      cards[optionTwoId].removeEventListener("click", flipCard);
      cardsWon.push(cardsChosen);
    } else { // 카드를 연속으로 빠르게 누르면 연속해서 같은 값이 입력되는 버그를 해결하기 위한 
      cards[optionOneId].setAttribute("src", "src/images/blank.png");
      cards[optionTwoId].setAttribute("src", "src/images/blank.png");
      alert("Sorry Try Again");
    }
```
