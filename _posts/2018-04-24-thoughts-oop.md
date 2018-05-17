---
layout: post
title: Object Oriented Programming and Design
category: Thoughts
tags: OOD OOP
---

자바는 객체지향 언어이다. 자바를 배우기 전에도 알았던 사실이지만 이 말이 의미하는 것이 무엇인지 얼마 전까지 몰랐다. 다음은 김종민씨의 <스프링 입문을 위한 자바 객체 지향의 원리와 이해>와 조영호씨의 <객체 지향의 사실과 오해>의 내용을 정리한 우아한 형제들 기술 블로그 (http://woowabros.github.io/study/2016/07/07/think_object_oriented.html)를 읽고 조금이나마 이해한 것, 그리고 지금까지 코드스쿼드에서 배우면서 느낀 점, 배운 점들을 정리한 내용이다.

---

### 객체 지향 정리

객체는 각자가 '책임'을 가지고 있고 서로 '협력'한다. 처음 이 단어들을 봤을 때는 너무 추상적이여서 무슨 말인지 전혀 감이 오지 않았다. 그러나 점점 객체 지향에 대해서 읽고 배운 내용들을 미션 진행을 하면서 적용해보니 조금씩 감이 오기 시작했다. 캡상추다를 외우기 쉬운 순서가 아닌 내가 생각하는 설계과정에서의 순서인 '추캡상다'로 정리해보았다.

#### 추:
현실 세계에서 인간은 추상화를 통해 모든 것을 분류한다. 예를 들면 '수학'이라던지, '자동차'나 '사람'이 있다. 컴퓨터 언어의 발전은 점점 인간이 읽고 쓰기 편리하도록 발전해 왔다. 인간이 이해할 수 없는 기계어에서 어셈블리어, 현재의 C, java와 python 같은 인간이 이해하기 쉬운 언어까지, java 객체 지향 패러다임은 이 트랜드를 따라 한 단계 더 인간에게 가까운 언어가 되는 것 이라고 생각한다. 인간이 현실에서 추상화를 하듯, 프로그래머가 프로그램에 필요한 요소들을 추상화해서 객체를 도출한다. 하지만 현실에서 추상화 하듯이 모든 것이 완벽하게 추상화가 될 수 없고 또 너무 현실에 빗대어 추상화를 한 나머지 over-engineering을 해서 코드가 더 복잡해 지는 것을 조심해야 한다. 핵심은 프로그램 요구상항을 잘 살펴보고 적절한 객체들을 추출하고 필요한 속성들만을 객체에 부여하는 것이다.

#### 캡:
예전에는 정보의 은닉이 필요한지 전혀 이해가 가지 않았다. 그저 '관련된 속성과 함수들을 묶고 밖에서 외부 조작을 하지 못하도록 접근제어자를 통해 접근은 제한한다' 정도로 알고 있었다. 하지만 조작을 하지 못하게 한다는건 왜 그럴까? 프로그래머가 어떤 메서드나 필드가 어디서 어떻게 쓰이는지 알고 있으면 문제 없는 게 아닌가? 하지만 규모마 커지면 커질수록 그런걸 다 염두해 두는 것이 힘들어질 뿐더러 한명의 프로그래머만 있는 게 아니라 여러 프로그래머가 협업한다는 것을 감안하면 해당 API를 만드는 입장에서 API의 잘못된 사용으로 의도치 않은 일의 발생 방지는 필수다. 

객체 지향의 핵심은 객체가 각자 하나의 책임을 부여받고 서로 메시지(요청/응답)을 주고 받으며 협력해야 한다는 것이다. 따라서 객체의 상태를 바꾸는 주체는 외부의 객체가 아닌 바로 그 객체여야 한다. 만약 메서드나 필드가 접근제한이 되어있지 않거나 getter와 setter를 사용하면 객체의 상태값을 바꾸는 주체는 그 객체가 아닌 외부 객체이다. 접근 제한이 되어있지 않다면 심각한 문제를 야기할 수 있다. 또 로직에 너무 getter/setter를 남발하면 의도치 않은 상태변경에 의해 예상과 다른 결과가 나올 수 있으며 발생된 문제를 해결할 때 어디서 어떻게 상태가 바뀌는지 추적하는 데에 어려움을 겪게된다. setter 없이 코딩하는 건 충분히 가능하고 getter도 정말 필요할 때 말고는 쓰지 않는 게 좋다.


#### 상/다:
코드 상 상속의 핵심적인 역할은 중복의 제거라고 생각한다. 컴퓨터 언어는 인간스러운 형태로 발전함과 동시에 코드의 중복을 최소화 시키는 방향으로도 발전했다. 공유하는 속성과 메서드는 상속을 통해 물려 받아서 재사용이 가능하므로 중복이 제거된다. 하지만 클래스 간의 추상적 관계를 고려하지 않고 단순히 중복을 제거하려는 목적으로만 상속을 하는 것은 바람직 하지 않다고 생각한다. 추상화 관점에서의 상속은 is a kind of relationship을 표현하기 때문에 클래스들이 상속관계에 맞는다고 생각되면 상속을 통해 자연스럽게 중복이 없어지는 것 같다.

다형성이란 같은 상위 타입의 객체가 똑같은 요청을 보냈을 때 서로 다른 응답을 받는 것이다. 같은 타입이지만 때에 따라 다른 behavior가 필요할 때 인터페이스/클래스 상속 및 오버라이딩을 통해 이러한 다형성을 구현할 수 있다. 다형성의 핵심은 같은 타입의 변수에 그 타입의 맞는 부품화된 객체를 담을 수 있다는 것이다. 상속을 통한 다형성의 예로, 같은 '나무' 타입이지만 '가을'이라는 변화에 어떤 나무는 붉게 물들고 또 어떤 나무는 초록색을 그래도 유지하는 것을 표현할 수 있겠다. 인터페이스로도 표현이 가능하겠지만 인터페이스는 다형성을 가능케 함과 동시에 캡슐화 성질은 한 단계 더 나아간 것 같다. 객체간의 협력 관계에 있어서 필요한 메서드만 사용할 수 있도록 일종의 '창구'를 만들어서 다형성을 제공한다. 예를 들면, '원숭이' 객체는 '나무' 객체가 가을에 붉게 물드는지 아닌지 알(메서드 사용할) 필요가 없다. 탈 수 있는 나무인지 아닌지만을 필요로 하기 때문에 'Climable' 인터페이스를 통해 두 나무 객체에게 'climb()'를 할 수 있는 것이다. 한 나무는 가지가 너무 약해서 '떨어짐'이란 결과가 나올 수 있고, 다른 나무는 '튼튼하지만 가시가 있어서 느림'이란 결과가 나올 수도 있다.

---

### 볼링 미션

아이러니하게도 인간친화적 패러다임에 맞게 코딩을 하는 것은 인간친화적이지 않은 것 같았다. 인간은 추상화를 통해 세상인 인지하지만 코딩은 또 절차적으로 하는 게 본능임을 깨달았다. 하지만 여러 제약사항을 걸어두고 (getter/setter 쓰지않기, 인덴트 한단계만 허용, else 안쓰기, 일급 콜렉션 쓰기, 모든 instance변수 private, 메서드 10줄 이하 등) 계속 연습하다 보니 어느정도 설계 사고가 바뀐 듯 하다. 

이번에 볼링 점수판을 구현하면서 배운게 정말 많다. 코드의 중복을 어떻게 줄이는지, 객체 간의 관계를 어떻게 정의하고 설계하는지, 어떻게 각 객체가 SOLID 원칙을 반영하도록 하고 필요에 의해 새로운 객체를 추출하는지 예전보다 조금 더 명확해 졌다.

처음엔 '까짓거 어려우면 얼마나 어렵겠어'라는 생각으로 시작했다. 하지만 이번 미션을 객체 지향적으로, TDD로 개발하려고 하니 절대 만만하지 않았다. 초기에는 추상화 단계를 프레임까지만 가져갔었다:

~~~java
public class Frame {
	private int first;
	private int second;
	
	public updateScore(int pinsKnocked){
		if//첫번째 투구가 진행 안됐을 경우
			this.first = pinsKnocked;
		if//첫번째 투구가 진행 됐을 경우
			this.second = pinsKnocked;
	}
	
	@Override
	public String toString(){
		if//투구가 아직 진행되지 않은 경우
		if//스트라이크인 경우
		if//스트라이크가 아니고 첫번째 투구만 진행된 경우
		if//스페어인 경우
		if//두번째 투구가 진행된 경우
	}
}
~~~

`if`문이 한 다여섯 개 정도면 조금 많기는 하지만 봐줄 수 있지 않을까..? 하지만 생각해 보면 투구가 진행되지 않은 건 어떻게 판단할 것이며 투구가 `0 < first||second < 10` 을 만족시켜야 하고 `second > 10 - first`도 만족시켜야 한다. `int`를 `Integer`로 써서 `null`이면 플레이되지 않은 거라고 판단 할 수 있지만 직접 해보니 생각치 못한 곳에서 `null-pointer exception`이 나오는 등 **null을 쓰는 것은 정말 안좋은 습관인 것을 깨달았다.** 또, 유효성 검사에서도 if문이 추가된다. 

나중에 스코어를 계산할 때는 더 심해진다.

~~~java
	public int calculateFrameScore(Frame nextFrame){
		if//다음 프레임 투구가 아직 안됐으면 계산 X
		if//전프레임이 스트라이크, 다음 프레임 두번째 투구가 안끝났으면 계산 X
		if//전프레임이 스트라이크, 다음 프레임 두번재 투구가 끝났으면 계산 O
		if//전프레임이 스페어, 다음프레임 첫번째 투구가 안끝났으면 계산 X
		if//전프레임이 스페어, 다음프레임 첫번째 투구가 끝났으면 계산 O
		if//전프레임 노멀이면 계산 O
	}
~~~
이런식으로 `if`문을 하나의 클래스에 남발하게 되었다. 생각치 못한 경우에 수가 아마 있을 것이다. 여기서 끝이 아니였다. 스트라이크면 `first + 다음 두 투구의 점수`, 스페어면 `first + second + 다음 투구의 점수`, 둘 다 아니면 그냥 `first + second`.. 또, 스트라이크가 두번 연속으로 나오면 다다음 프레임의 첫번째 투구가 끝날 때 까지 점수계산이 불가능 하도록 로직을 만들어야 한다. 또! 마지막 프레임은 스트라이크/스페어가 나오면 보너스 투구가 이루어져야하고 점수 계산법도 다르다. 고작 볼링점수 계산하는 게 뭐 그리 어려울까 생각되었지만.. 정말 엄청났다.

물론 위와 같은 방식으로도 충분히 구현 할 수 있다. 수많은 `if`문과 모든 경우의 수, 예외 상황을 추적하기 위한 코드만큼 긴 주석들을 통해서.. 이렇게 구현된 코드를 다른 사람이 읽었을 때 읽고 싶을까? 아니라는 생각이 든다. 만약 다른 요구사항이 추가됐을 경우, 예를 들어 `"0"`대신 `"-"`을 표시해야 한다면..? `if`가 더 추가된다.

**여기서 내가 배운 점은 하나의 메소드나 클래스 내에서 `if`문으로 분기가 많아지면 클래스 분리, 즉 또 다른 객체의 추상화가 필요한 시점인지 의심해봐야 한다.** 추상화을 더 세분화해서 하면 `if`가 여러 곳으로 분산되면서 생각할 경우의 수가 현저히 줄면서 가독성이 증가하고 **요구사항이 변경되었을 때 변경포인트를 한 곳으로 가져갈 수 있다.**

이 시점에서 필요한 것은 추상화라는 것을 깨닫고 추출된 객체가 각 프레임이 스트라이크인지 스페어인지 보통 숫자(Miss)인지의 상태를 표현하는 'Status'라는 interface와 Strike/Spare/Miss/FirstBowl 구현체다. 추상화를 한 단계 더 하고 나니 조건문이 분산되고 생각해야하는 경우의 수가 줄면서 테스트도 훨씬 편하면서 문제 추적이 용이하고 변경에 유연한 코드가 나왔다. 

볼링 미션을 하면서 정말 많은 insight를 얻었고 객체 지향에 대한 감이 어느정도 생긴 것 같다. 지금까지 배운 점들을 토대로 예전에 했던 미션들을 다시 해볼 생각이다.
