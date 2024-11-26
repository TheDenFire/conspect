**General responsibility Assignet Software Patterns**
Общие паттерны распределения обязанностей в ПО

## **Информационный эксперт - Information expert** 
Тип, имеющий максимум информации, имеет ответственность выполнения операций над этим типом - информационный эксперт. 

Недостатки
Паттерн подрозумевает то, что логика обработки и изменения информации, хранимой обьектом, должна происходить непосредственно в самом типе обьекта. В огромной системе, где тип сам по себе большой, он будет забит всевозможными методами к его атрибутам, нежели определением поведений которыми тип характеризуется. 

## **Создатель - Creator**
Обьект, создающий другие обьекты. Паттерн определяет правила, которым должны следовать обьекты, обладающие характеристикой создателя. 

Благодаря строителю, созданные обьекты ассоциированы с создателем
Создатель использует созданные обьекты 
Создатель знает как инициализировать создаваемые обьекты, обладая нужными для этого атрибутами

Напримир Builder, Factory method, Abstract factory

## **Контроллер - Controller**
Паттерн предполагающий наличие типа, не принадлежащего пользовательскому интерфейсу, обрабатывабщего системные события/запросы. Является частью MVC паттерна, мостом между View и Model

Виды контроллеров:
Use-case сontroller
	Контроллер инкапсулирующий логику обработки какого-то конкретного события/запроса
Use-case-group controller
	Контроллер обрабатывающий группу событий/запросов, имеющий общий скоуп
Controller-Facade
	Контроллер предоставляющий доступ ко всем операциям подразумевающимся системой.
```C#
public class AddUserController 
{
		private readonly IUserService _userService;

		// ...

		public void AddUser(User user)
		{
				_userService.AddUser(user);
		}
}

public class UserController
{
		private readonly IUserService _userService;

		// ...

		public void AddUser(User user)
		{
				_userService.AddUser(user);
		}

		public void DeleteUser(UserId id)
		{
				_userService.DeleteUser(id);
		}
}


public class FacadeController
{
		private readonly IUserService _userService;
		private readonly IMailingService _mailingService;

		// ...
}
```

## **Слабая связанность - Low Coupling**
Связанность, от слова связать.
	Coupling defree - мера зависимость типов друг от друга
Принцип подразумевающий минимизацию зависимости между проектирууемыми модулями кода.

Достигается добавлением в систему абстракций, в результате которого, модули не зависят от других конкретных модулей, и могут принимать различные реализации данной абстракции.
Использование интерфейсов и абстракций может помочь минимизировать соединение и повысить возможность повторного использования кода.

**Сильная связность - High cohesion** 
Связность, от слова связно (говорить связно)
Оценочный паттерн, направленный на то, чтобы держать обьекты сфокусированными на выполнении возложенного на них функционала. Этот паттерн является аналогом Single Responsibility Principle SRP из SOLID

## **Indirection** 
Один из способов уменьшить связанность модулей.

Виды реализации
	Вместо вызова у конкретного модуля, вызов идет к посреднику
	Любая абстракция над структурой обьектов (TotalCost в классе Customer)
	Паттерн декоратор и прокси

**Полиморфизм - Polymorphism**
Вместо ветвления логики основываясь на типе, на флагах, хранящихся в обьекте, выделите общий интерфейс и используйте полиморфные операции для достижения результата. 

## **Protected Variations** 
Принцип, заключающийся в выделении точек имеющих наибольший потенциал к изменению на этапе проектирования системы. Реализация частей системы, склонных к изменению, должна подразумевать не только текущую логику, но и возможность эту логику заменить на какую-либо другую. 
Тут входит абстракция. Суть в проектировании стабильного интерфейса над потенциально не стабильной реализацией. 

## **Pure Fabrication** 
Подход, заключающийся в том, что мы можем добавить в нашу модель системы типы не отражающие какие-то сущности или примитивы моделируемого домена (полностью выдуманные). 
Такие классы зачастую называют сервисами, они могут инкапсулировать какую-либ инфраструктурную логику, не являющиюся отражением предметной области, но все еще необходимую для работы приложения, какие либо сценарии использования приложения, являющиеся последовательностью выполнения доменных операций.
Последние называются сервисами приложения и позволяют снизить связанность между сущностями. 

Принцип чистого изготовления предполагает создание искусственных классов для улучшения проектирования системы. Эти классы не связаны напрямую с доменом или решаемой проблемой, а служат помощниками или связующими звеном между другими классами. Pure Fabrication помогает достичь низкой связи и высокой сплоченности путем инкапсуляции сложных операций или предоставления интерфейса к внешним системам.