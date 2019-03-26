---
layout: post
title: Core-Data-Tutorial
date: 2019-03-26
excerpt: "Core Data 튜토리얼"
tag:
- swift
comments: true
---

# Core Data Tutorial

> [Getting Started with Core Data Tutorial]([https://www.raywenderlich.com/7569-getting-started-with-core-data-tutorial](https://www.raywenderlich.com/7569-getting-started-with-core-data-tutorial)) 을 참고하였습니다. 많이 부족하지만 거의 번역에 가까우며 공부하며 정리한 내용입니다. 자세한 원본 내용은 해당 사이트를 참고하시는 것이 좋습니다.

> 제 [github](https://github.com/chelwoong/CoreData-Tutorial)을 통해 해당 파일을 보실 수 있습니다.

## Core Data 사용하기

Xcode 생성 시에 **Use Core Data** 를 체크해서 프로젝트를 생성한다. 이렇게 하면 **AppDelegate.swfit**에 `NSPersistentContainer` 를 생성해준다. 

NSPersistentContainer 는 Core Data에서 정보를 저장하고 검색하는 것을 쉽게 해주는 객체들의 집합이다.

기본적으로 대부분의 앱에서 잘 작동하지만 앱 및 데이터 요구사항에 따라 효율적으로 커스터마이징이 가능하다. 

> 모든 Xcode 템플릿이 Core Data를 지원하지는 않는다. **Xcode 10**에서는 **Master-Detail App** 과 **Single View App** 에서만 **Use Core Data**를 선택할 수 있다.

이 튜토리얼은 Single View App으로 만들었으며, 매우 간단하다. "Hit List"라는 tableView가 있고 여기에 이름을 추가할 수 있다. Core Data를 사용해 세션간에 저장이 가능하다. 

**기본적으로 tableView를 생성하고 UIAlertController를 사용해 이름을 입력받는 과정은 생략하겠다. 여기서는 어떻게 Core Data를 사용하는지에 대해서만 집중적으로 다뤄보도록 하겠다.**

## Data Modeling 하기

첫번째 단계는, Core Data의 데이터 모델을 관리하는 managed object model을 만드는 것이다. 

Core Data는 기본적으로 SQLite 데이터 베이스를 영구 저장소로 사용하므로 데이터 모델을 데이터 베이스 스키마로 생각할 수 있다. 

Use Core Data를 선택해 앱을 생성하면 자동적으로 .xcdatamodeld라는 파일이 생성되어 있다. 

[](https://www.notion.so/5ad15fb23d6f46aea2df2ff3273c2980#52e6fea9b17b498697ff06602d30a922)

하단의 Add Entity, Add Attribute 등을 사용해 Entity와 Attribute를 추가할 수 있다. 

- Entity는 Core Data의 클래스 정의다. 관계형 데이터 베이스의 Table과 같다. 대표적인 예로 회사, 직원 등을 생각하면 된다.
- Attribute는 entity에 첨부된 정보다. 관계형 데이터 베이스 Table의 특정 필드에 해당한다. 대표적인 예로 직원의 이름, 직위 및 급여 등을 떠올리면 된다.
- Relationship는 Core Data에서 entity 끼리의 관계를 나타낸다. 두 entity간의 관계는 **일대일 관계** 라고 불리는 반면, 하나의 entity와 여러 entity끼리의 관계는 **일대다 관계**라고 불립니다. 예를 들어, 관리자는 직원들과 **일대다 관계**를 갖지만, 보통 직원은 관리자와 **일대일 관계**를 갖는다.

## Core Data에 저장하기

Core Data를 사용하기 위해 우선 ViewController.swift에 import 한다.

    import CoreData

`NSManagedObject` 객체 배열을 생성한다. 

    var people: [NSManagedObject] = []

`NSManagedObject`는 Core Data에 저장된 단일 객체를 나타낸다. Core Data를 생성, 수정, 편집, 저장, 삭제 등을 하기 위해 반드시 이 객체를 사용해야 한다. `NSManagedObject`는 임의의 entity를 나타낼 수 있기 때문에 **shape-shifter라고 불린다**. 정의한 속성 및 관계를 사용해 모든 형식의 entity를 취할 수 있다.

이제 이를 사용해 tableView를 조금 수정해야 한다.

    // MARK: - UITableViewDataSource
    extension ViewController: UITableViewDataSource {
      func tableView(_ tableView: UITableView,
                     numberOfRowsInSection section: Int) -> Int {
        return people.count
      }
    
      func tableView(_ tableView: UITableView,
                     cellForRowAt indexPath: IndexPath)
                     -> UITableViewCell {
    
        let person = people[indexPath.row]
        let cell =
          tableView.dequeueReusableCell(withIdentifier: "Cell",
                                        for: indexPath)
        cell.textLabel?.text =
          person.value(forKeyPath: "name") as? String
        return cell
      }
    }

`NSManagedObject`에서 attribute를 가져오는 방법은 다음과 같다.

    cell.textLabel?.text =
      person.value(forKeyPath: "name") as? String

왜 이렇게 해야할까? `NSManagedObject`에서는 name **attribute를 알지 못한다.** 따라서 속성을 직접적으로 가져올 수 없다. Core Data는 **key-value coding**을 통해서만 값을 읽을 수 있다. 이러한 방법을 **KVC**라고 한다. 

다음으로 값을 저장하는 방법을 살펴보자. 값을 저장하는 save 함수이다. 

    func save(name: String) {
      
      guard let appDelegate =
        UIApplication.shared.delegate as? AppDelegate else {
        return
      }
      
      // 1
      let managedContext =
        appDelegate.persistentContainer.viewContext
      
      // 2
      let entity =
        NSEntityDescription.entity(forEntityName: "Person",
                                   in: managedContext)!
      
      let person = NSManagedObject(entity: entity,
                                   insertInto: managedContext)
      
      // 3
      person.setValue(name, forKeyPath: "name")
      
      // 4
      do {
        try managedContext.save()
        people.append(person)
      } catch let error as NSError {
        print("Could not save. \(error), \(error.userInfo)")
      }
    }

각 코드의 기능을 자세히 살펴보자.

1. Core Data에 값을 저장하거나 탐색하기 전에 우선 NSManagedObjectContext가 필요하다. 이를 객체 작업을 위한 메모리 내의 'scratchpad'라고 생각할 수 있다.
 
새로운 관리 managed object를 만드는 방법을 두 단계로 생각해보자. 우선 managed object를 managed object context에 넣는다. managed object context를 디스크에 저장할 수 있도록 'commit'해야 마음을 놓을 수 있다.

Use Core Data를 선택해서 프로젝트를 생성했다면, Xcode는 이미 새 템플릿을 생성할 때 managed object context를 일부로 만들었다. 이 기본 managed object context는 application delegate안에 NSPersistentContainer의 속성으로 살아있다. 여기에 접근하기 위해 app delegate의 레퍼런스를 참조해야 한다. 
2. 앞의 과정을 통해 새로운 managed object를 가진 managed object context를 생성했다면, `NSManagedObject`의 static method인 `entity(forEntityName:in:)`을 사용할 차례다. 

NSEntityDescription에 대해 궁금할 수 있다. 앞서 NSManagedObject는 임의의 엔티티를 나타낼 수 있기 때문에 shape-shifter라고 불린다고 했었다. EntityDescription은 런타임시에 데이터 모델의 entity 정의와 NSManagedObject의 인스턴스를 연결하는 부분이다. 
3. 이제 얻은 NSManagedObject를 사용해, key-value coding을 사용해 name attribute를 설정한다. 반드시 KVC 키(이 경우에는 name)이 Data Model 에 있는 것과 **정확히 일치**해야 한다. 그렇지 않으면 런타임시 충돌이 발생한다. 
4. 이제 바뀐 부분을 person에 넣고 디스크에 저장하기 위해서 managed object context의 `save`를 호출한다. `save`는 error가 발생할 수 있기 때문에 `do-catch` 블록 안에 `try`를 사용해야 한다는 것에 주의하자. 마침에 새로운 managed object이 person에 저장되었으니 tableView를 reload하자. 

여기까지 해서 우리는 Core Data에 data를 저장하는데 성공했다. 여기까지만 하면 끝일까?

여기까지만 한다면, 앱을 종료 후 재 실행 했을 때 값이 비어있다. 잘 저장은 했지만 disk에서 읽어들이지 못하고 있기 때문이다. 

## Core Data 에서 가져오기

영구 저장소에 있는 데이터를 managed object로 가져오기 위해서 `fetch`를 사용해야 한다. viewDidLoad()에 다음을 추가해보자.

    override func viewWillAppear(_ animated: Bool) {
      super.viewWillAppear(animated)
      
      //1
      guard let appDelegate =
        UIApplication.shared.delegate as? AppDelegate else {
          return
      }
      
      let managedContext =
        appDelegate.persistentContainer.viewContext
      
      //2
      let fetchRequest =
        NSFetchRequest<NSManagedObject>(entityName: "Person")
      
      //3
      do {
        people = try managedContext.fetch(fetchRequest)
      } catch let error as NSError {
        print("Could not fetch. \(error), \(error.userInfo)")
      }
    }

코드를 자세히 살펴보자.

1. 앞서 Core Data를 가져오기 위해 무엇이 필요했을까? 맞다. managed object context가 필요했었다. fetch라고 다르지 않다. 똑같이 가져오자.
2. 이름에서 알 수 있듯이 `NSFetchRequest`는 Core Data에서 fetching을 담당한다. Fetch request는 강력하고 유연하다. 이를 통해 기준을 충족하는 객체 집합을 가져올 수 있다. 

fetch request에는 return 값을 구체화 하기 위한 몇 가지 한정자가 필요하다. 여기처럼NSEntityDescription이 그 중 하나이다.

fetch request의 entity 속성을 설정하거나, `init(entityName:)`으로 초기화 하면 특정 엔티티의 모든 객체를 가져온다. 또한 `NSFetchRequest`는 generic 타입임에 주목하자. 이 generics를 사용하면 return 타입을 지정할 수 있다. ( 이 경우 `<NSManagedObject>` 이다. )
3. 헤비한 과정을 수행하기 위해 fetch request는 managed object context에 값을 넘겨준다. fetch(_:)는 지정된 요청에 충족하는 managed objects 배열을 반환한다.

### Key Points

- Core Data는 **on-disk persistence**를 제공해서 앱이 종료되거나 기기를 종료한 후에도 데이터에 접근할 수 있다. 이것은 in-memory persistence와는 다른데, 이는 앱이 포그라운드 또는 백그라운드에서 메모리에 있는 동안에만 데이터를 저장한다.
- Xcode에는 강력한 **Data Model editor**가 제공되며, 이를 사용해 **managed object model**을 만들 수 있다.
- managed object model은 **entity, attribute, relationships**로 구성된다.
- **entity**는 Core Data의 클래스 정의다.
- **attribute**는 entity에 첨부된 정보다.
- **relationships**는 여러 entity 간의 연결이다.
- `NSManagedObjec`t는 Core Data의 런타임 표현이다. **Key-Value Coding**을 사용해 읽고 쓸 수 있다.
- `save()`나 `fetch(_:)`를 하기 위해서는 `NSManagedObjectContext`가 필요하다.