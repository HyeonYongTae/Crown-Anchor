
    function rand(m, n) { //(3,  20)
        return m + Math.floor((n - m + 1) * Math.random()); ->  3 + Math.floor(x > 0 && x < 18) x 
      }

	Math.floor() 함수는 주어진 숫자와 같거나 작은 정수 중에서 가장 큰 수를 반환한다.(내림)
	Math.random() 함수는 0 이상 1 미만의 구간에서 근사적으로 균일한(approximately uniform) 부동소숫점 의사난수를 반환하며, 
	이 값은 사용자가 원하는 범위로 변형할 수 있다.


      // 크라운 앤 앵커 게임의 여섯 그림 중 하나에 해당하는 문자열을 무작위로 반환한다.
    function randFace() {
        return ["crown", "anchor", "heart", "spade", "club", "diamond"]
          [rand(0, 5)];
      }

	[배열][index] = 그 인덱스의 요소 값

      console.log(rand(1, 100));
      console.log(randFace());

      let funds = 50; // 시작 조건  돈이 처음에 50원
      let round = 0;  // 라운드 변수 선언해주고 0 할당

      while(funds > 1 && funds < 100) {
        round++; // 라운드 1씩 증가

        console.log(`round ${round}`);
        console.log(`\tstarting funds: ${funds}p`);
        // 돈을 건다
        let bets = { crown: 0, anchor: 0, heart: 0,
                     spade: 0, club: 0, diamond: 0 };

        let totalBet = rand(1, funds); // 1이상 50이하 랜덤한 숫자
        if (totalBet === 7) {
          totalBet = funds; //전재산
          bets.heart = totalBet; //하트에 배팅 전재산
        } else {
            //판돈을 나눈다.
            let remaining = totalBet;

            do {
                let bet = rand(1, remaining);
                let face = randFace(); // 랜덤한 문양
                bets[face] = bets[face] + bet; // 문양에 돈을 검
                remaining = remaining - bet; // 돈을 걸고 남은 돈
            } while(remaining > 0)
        }
        funds = funds - totalBet; //배팅한 후 자금
        console.log('\tbets: ' +

        Object.keys(bets).map(face => `${face}: ${bets[face]} pence`).join(', ') +
        `(total: ${totalBet} pence)`);

		Object.keys(obj) – 객체의 키만 담은 배열을 반환한다.
		Object.keys(bets) ['crown','anchor','heart','spade','club','diamond']


        //주사위를 굴린다.
        const hand = [];
        for (let roll = 0; roll < 3; roll++) {
            hand.push(randFace());			//주사위를 굴려서 문양 뽑기
        }
        console.log(`\thand: ${hand.join(', ')}`);

        //딴 돈을 가져온다.
        let winnings = 0;

        for (let die = 0; die < hand.length; die++) {
            let face = hand[die];
            if(bets[face] > 0) winnings = winnings + bets[face];
        }
        funds = funds + winnings;
        console.log(`\twinnings: ${winnings}`);
      }

      console.log(`\tending funds: ${funds}`);



