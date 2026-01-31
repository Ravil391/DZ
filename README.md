Домашнее задание
Уровень 1
Задание 1
Создайте следующую структуру классов:
1. Базовый класс Transport
Свойства:
public string Model { get; set; }
protected int Speed — скорость (начальное значение 0)


Методы:
public void ShowInfo() — выводит:
 "Модель: {Model}, скорость: {Speed} км/ч"
public virtual void Move() — выводит "Транспорт движется".

2. Класс Car, наследник Transport
Добавьте:
метод public void Accelerate(int value), который увеличивает Speed на value, но не более чем до 200. (Если значение больше — выведите сообщение "Слишком большая скорость!")
переопределите метод Move() (override) → "Машина едет по дороге".

3. Класс Bicycle, наследник Transport
Добавьте:
метод public void Pedal() — увеличивает Speed на 5;
переопределите метод Move() → "Велосипед крутит педали".

Пример использования:
var car = new Car { Model = "Audi" };
car.Accelerate(100);
car.ShowInfo();
car.Move();

var bike = new Bicycle { Model = "Cube" };
bike.Pedal();
bike.ShowInfo();
bike.Move();


Ожидаемый результат:
Модель: Audi, скорость: 100 км/ч
Машина едет по дороге
Модель: Cube, скорость: 5 км/ч
Велосипед крутит педали












































using System;
public class Transport
{
    public string Model { get; set; }
    protected int Speed { get; set; } = 0;

    public void ShowInfo()
    {
        Console.WriteLine($"Модель: {Model}, скорость: {Speed} км/ч");
    }

    public virtual void Move()
    {
        Console.WriteLine("Транспорт движется");
    }
}
public class Car : Transport
{
    public void Accelerate(int value)
    {
        if (Speed + value > 200)
        {
            Console.WriteLine("Слишком большая скорость!");
        }
        else
        {
            Speed += value;
        }
    }
    public override void Move()
    {
        Console.WriteLine("Машина едет по дороге");
    }
}
public class Bicycle : Transport
{
    public void Pedal()
    {
        Speed += 5;
    }
    public override void Move()
    {
        Console.WriteLine("Велосипед крутит педали");
    }
}







Уровень 2
Задание 2
1. Создайте абстрактный класс Character
Содержит:
свойство Name;
абстрактный метод:


public abstract void Attack();


2. Создайте наследников
Каждый реализует метод Attack():
Warrior — "Воин атакует мечом!"
Mage — "Маг выпускает огненный шар!"
Archer — "Лучник стреляет из лука!"


Пример:
Character[] team =
{
    new Warrior { Name = "Алекс" },
    new Mage { Name = "Лия" },
    new Archer { Name = "Робин" }
};

foreach (var c in team)
{
    Console.Write($"{c.Name}: ");
    c.Attack();
}













public abstract class Character
{
    public string Name { get; set; }
    public abstract void Attack();
}

public class Warrior : Character
{
    public override void Attack()
    {
        Console.WriteLine("Воин атакует мечом!");
    }
}

public class Mage : Character
{
    public override void Attack()
    {
        Console.WriteLine("Маг выпускает огненный шар!");
    }
}

public class Archer : Character
{
    public override void Attack()
    {
        Console.WriteLine("Лучник стреляет из лука!");
    }
}






















class Program
{
    static void Main()
    {
        // Уровень 1
        var car = new Car { Model = "Audi" };
        car.Accelerate(100);
        car.ShowInfo();
        car.Move();

        var bike = new Bicycle { Model = "Cube" };
        bike.Pedal();
        bike.ShowInfo();
        bike.Move();

        Console.WriteLine(); // Разделитель

        // Уровень 2
        Character[] team =
        {
            new Warrior { Name = "Алекс" },
            new Mage { Name = "Лия" },
            new Archer { Name = "Робин" }
        };

        foreach (var c in team)
        {
            Console.Write($"{c.Name}: ");
            c.Attack();
        }
    }
}
















Домашнее задание
Уровень 1
Задание 1
1. Создайте абстрактный класс Worker:
свойство Name;
абстрактный метод Work();
метод ShowInfo() — выводит "Работник: {Name}".


2. Создайте классы, унаследованные от класса Worker:
Manager с реализованным методом Work() — "Планирует задачи";
Developer с реализованным методом Work() — "Пишет код".


Пример:
Worker[] workers = { new Manager { Name = "Анна" }, new Developer { Name = "Иван" } };
foreach (var w in workers)
{
    w.ShowInfo();
    w.Work();
}




















using System;
public abstract class Worker
{
    public string Name { get; set; }

    public abstract void Work();

    public void ShowInfo()
    {
        Console.WriteLine($"Работник: {Name}");
    }
}

public class Manager : Worker
{
    public override void Work()
    {
        Console.WriteLine("Планирует задачи");
    }
}

public class Developer : Worker
{
    public override void Work()
    {
        Console.WriteLine("Пишет код");
    }
}
class Program
{
    static void Main()
    {
        Worker[] workers = { 
            new Manager { Name = "Анна" }, 
            new Developer { Name = "Иван" } 
        };

        foreach (var w in workers)
        {
            w.ShowInfo();
            w.Work();
        }
    }
}






Уровень 2
Задание 2
Создайте абстрактный класс CookingProcess. Класс должен описывать общий алгоритм приготовления блюда:
подготовка ингредиентов,
основной процесс приготовления,
подача готового блюда.
Создайте два класса, например Soup и Steak, которые наследуются от CookingProcess. Каждый из этих классов должен по-своему определять, что происходит на основном шаге приготовления.
Для супа нужно описать, что он варится.
Для стейка — что он жарится.


Эти классы должны заполнить абстрактный шаг процесса, но при этом использовать уже готовые шаги подготовки и подачи, которые находятся в базовом классе.



















using System;

public abstract class CookingProcess
{
    public void PrepareIngredients()
    {
        Console.WriteLine("Подготовка ингредиентов: моем, режем, чистим.");
    }
    public abstract void Cook();
    public void Serve()
    {
        Console.WriteLine("Подача: выкладываем на тарелку и украшаем.");
    }
}

public class Soup : CookingProcess
{
    public override void Cook()
    {
        Console.WriteLine("Процесс: ингредиенты варятся в кастрюле на медленном огне.");
    }
}

public class Steak : CookingProcess
{
    public override void Cook()
    {
        Console.WriteLine("Процесс: мясо жарится на раскаленной сковороде до нужной прожарки.");
    }
}
class Program
{
    static void Main()
    {
        Console.WriteLine("--- Готовим Суп ---");
        CookingProcess soup = new Soup();
        soup.PrepareIngredients();
        soup.Cook();
        soup.Serve();
        Console.WriteLine("\n--- Готовим Стейк ---");
        CookingProcess steak = new Steak();
        steak.PrepareIngredients();
        steak.Cook();
        steak.Serve();
    }
}
Домашнее задание
Уровень 1 
Выполнить задания из практики.
Шаг 1. Создайте класс Издательство с полем названия и методом вывода информации о нём.
public class PublishingHouse
{
    public string Name { get; set; }

    public PublishingHouse(string name)
    {
        Name = name;
    }

    public void ShowInfo()
    {
        Console.WriteLine($"Издательство: {Name}");
    }
}


Шаг 2. Создайте класс Книга с приватными полями: название, автор, год издания, количество страниц. Реализуйте конструкторы и свойства с проверками. Добавьте метод для вывода информации о книге.
public class Book
{
    private string _title;
    private string _author;
    private int _year;
    private int _pages;

    public string Title
    {
        get => _title;
        set
        {
            if (!string.IsNullOrEmpty(value)) _title = value;
        }
    }

    public string Author
    {
        get => _author;
        set
        {
            if (!string.IsNullOrEmpty(value)) _author = value;
        }
    }

    public int Year
    {
        get => _year;
        set
        {
            if (value > 0) _year = value;
        }
    }

    public int Pages
    {
        get => _pages;
        set
        {
            if (value > 0) _pages = value;
        }
    }

    public Book(string title, string author, int year, int pages)
    {
        Title = title;
        Author = author;
        Year = year;
        Pages = pages;
    }

    public virtual void ShowInfo()
    {
        Console.WriteLine($"Книга: {Title}, Автор: {Author}, Год: {Year}, Страниц: {Pages}");
    }
}


Шаг 3. Создайте классы-наследники Учебник и ХудожественнаяКнига с дополнительными полями (предмет и жанр). Переопределите метод вывода информации.
public class Textbook : Book
{
    public string Subject { get; set; }

    public Textbook(string title, string author, int year, int pages, string subject)
        : base(title, author, year, pages)
    {
        Subject = subject;
    }

    public override void ShowInfo()
    {
        Console.WriteLine($"Учебник: {Title}, Предмет: {Subject}, Автор: {Author}, Год: {Year}, Страниц: {Pages}");
    }
}

public class FictionBook : Book
{
    public string Genre { get; set; }

    public FictionBook(string title, string author, int year, int pages, string genre)
        : base(title, author, year, pages)
    {
        Genre = genre;
    }

    public override void ShowInfo()
    {
        Console.WriteLine($"Художественная книга: {Title}, Жанр: {Genre}, Автор: {Author}, Год: {Year}, Страниц: {Pages}");
    }
}


Шаг 4. Создайте класс Читатель с полями имя, ID и списком взятых книг. Реализуйте метод ВзятьКнигу, который добавляет книгу в список.

public class Reader
{
    public string Name { get; set; }
    public int Id { get; set; }
    private List<Book> _borrowedBooks = new List<Book>();

    public Reader(string name, int id)
    {
        Name = name;
        Id = id;
    }

    public void BorrowBook(Book book)
    {
        _borrowedBooks.Add(book);
        Console.WriteLine($"{Name} взял книгу \"{book.Title}\"");
    }

    public void ShowBorrowedBooks()
    {
        Console.WriteLine($"Книги у {Name}:");
        foreach (var book in _borrowedBooks)
        {
            book.ShowInfo();
        }
    }
}


Шаг 5. Создайте интерфейс ILibraryManagement с методами для добавления, удаления, поиска книг и вывода списка.
public interface ILibraryManagement
{
    void AddBook(Book book);
    bool RemoveBook(Book book);
    List<Book> SearchByAuthor(string author);
    void ListBooks();
}


Шаг 6. Создайте класс Библиотека, реализующий интерфейс, управляющий коллекцией книг. Добавьте методы выдачи книги читателю и возврата.
public class Library : ILibraryManagement
{
    private List<Book> _books = new List<Book>();

    public void AddBook(Book book)
    {
        _books.Add(book);
        Console.WriteLine($"Книга \"{book.Title}\" добавлена в библиотеку.");
    }

    public bool RemoveBook(Book book)
    {
        bool removed = _books.Remove(book);
        if (removed)
            Console.WriteLine($"Книга \"{book.Title}\" удалена из библиотеки.");
        return removed;
    }

    public List<Book> SearchByAuthor(string author)
    {
        return _books.Where(b => b.Author == author).ToList();
    }

    public void ListBooks()
    {
        Console.WriteLine("Список книг в библиотеке:");
        foreach (var book in _books)
        {
            book.ShowInfo();
        }
    }

    public void IssueBook(Book book, Reader reader)
    {
        if (_books.Contains(book))
        {
            reader.BorrowBook(book);
            _books.Remove(book);
        }
        else
        {
            Console.WriteLine($"Книга \"{book.Title}\" сейчас недоступна.");
        }
    }

    public void ReturnBook(Book book)
    {
        _books.Add(book);
        Console.WriteLine($"Книга \"{book.Title}\" возвращена в библиотеку.");
    }
}


Шаг 7. Создайте абстрактный класс Публикация с абстрактным методом ПолучитьИнформацию, реализуйте этот метод в классе-наследнике для книги.
public abstract class Publication
{
    public abstract void GetInfo();
}

public class BookPublication : Publication
{
    private Book _book;

    public BookPublication(Book book)
    {
        _book = book;
    }

    public override void GetInfo()
    {
        _book.ShowInfo();
    }
}


Шаг 8. Напишите сценарий использования
class Program
{
    static void Main()
    {
        Library library = new Library();

        Textbook t1 = new Textbook("Математика 101", "Иванов", 2020, 300, "Математика");
        FictionBook f1 = new FictionBook("Война и мир", "Толстой", 1869, 1200, "Роман");

        library.AddBook(t1);
        library.AddBook(f1);
        library.ListBooks();

        Reader reader = new Reader("Алексей", 1);

        library.IssueBook(t1, reader);
        reader.ShowBorrowedBooks();

        library.ListBooks();

        library.ReturnBook(t1);
        library.ListBooks();

        Publication pub = new BookPublication(f1);
        pub.GetInfo();
    }
}



























using System;
using System.Collections.Generic;
using System.Linq;

namespace LibrarySystem
{
    public class PublishingHouse
    {
        public string Name { get; set; }

        public PublishingHouse(string name)
        {
            Name = name;
        }

        public void ShowInfo()
        {
            Console.WriteLine($"Издательство: {Name}");
        }
    }

    public class Book
    {
        private string _title;
        private string _author;
        private int _year;
        private int _pages;

        public string Title
        {
            get => _title;
            set { if (!string.IsNullOrEmpty(value)) _title = value; }
        }

        public string Author
        {
            get => _author;
            set { if (!string.IsNullOrEmpty(value)) _author = value; }
        }

        public int Year
        {
            get => _year;
            set { if (value > 0) _year = value; }
        }

        public int Pages
        {
            get => _pages;
            set { if (value > 0) _pages = value; }
        }

        public Book(string title, string author, int year, int pages)
        {
            Title = title;
            Author = author;
            Year = year;
            Pages = pages;
        }

        public virtual void ShowInfo()
        {
            Console.WriteLine($"Книга: {Title}, Автор: {Author}, Год: {Year}, Страниц: {Pages}");
        }
    }

    public class Textbook : Book
    {
        public string Subject { get; set; }

        public Textbook(string title, string author, int year, int pages, string subject)
            : base(title, author, year, pages)
        {
            Subject = subject;
        }

        public override void ShowInfo()
        {
            Console.WriteLine($"Учебник: {Title}, Предмет: {Subject}, Автор: {Author}, Год: {Year}, Страниц: {Pages}");
        }
    }

    public class FictionBook : Book
    {
        public string Genre { get; set; }

        public FictionBook(string title, string author, int year, int pages, string genre)
            : base(title, author, year, pages)
        {
            Genre = genre;
        }

        public override void ShowInfo()
        {
            Console.WriteLine($"Художественная книга: {Title}, Жанр: {Genre}, Автор: {Author}, Год: {Year}, Страниц: {Pages}");
        }
    }

    public class Reservation
    {
        public Book Book { get; set; }
        public Reader Reader { get; set; }
        public DateTime ReservationDate { get; set; }
        public int ExpiryDays { get; set; }

        public Reservation(Book book, Reader reader, int expiryDays = 3)
        {
            Book = book;
            Reader = reader;
            ReservationDate = DateTime.Now;
            ExpiryDays = expiryDays;
        }

        public bool IsExpired() => DateTime.Now > ReservationDate.AddDays(ExpiryDays);
    }

    public class Reader
    {
        public string Name { get; set; }
        public int Id { get; set; }
        private List<Book> _borrowedBooks = new List<Book>();

        public Reader(string name, int id)
        {
            Name = name;
            Id = id;
        }

        public void BorrowBook(Book book)
        {
            _borrowedBooks.Add(book);
            Console.WriteLine($"{Name} взял книгу \"{book.Title}\"");
        }

        public void ShowBorrowedBooks()
        {
            Console.WriteLine($"Книги у {Name}:");
            foreach (var book in _borrowedBooks)
            {
                book.ShowInfo();
            }
        }
    }

    public interface ILibraryManagement
    {
        void AddBook(Book book);
        bool RemoveBook(Book book);
        List<Book> SearchByAuthor(string author);
        void ListBooks();
    }

    public class Library : ILibraryManagement
    {
        private List<Book> _books = new List<Book>();
        private List<Reservation> _reservations = new List<Reservation>();

        public void AddBook(Book book)
        {
            _books.Add(book);
        }

        public bool RemoveBook(Book book)
        {
            return _books.Remove(book);
        }

        public List<Book> SearchByAuthor(string author)
        {
            return _books.Where(b => b.Author == author).ToList();
        }

        public void ListBooks()
        {
            Console.WriteLine("\n--- Книги в библиотеке ---");
            foreach (var book in _books) book.ShowInfo();
        }

        public void ReserveBook(Book book, Reader reader)
        {
            if (_books.Contains(book))
            {
                _reservations.Add(new Reservation(book, reader));
                Console.WriteLine($"Книга \"{book.Title}\" зарезервирована для {reader.Name}");
            }
        }

        public void CancelReservation(Book book)
        {
            var res = _reservations.FirstOrDefault(r => r.Book == book);
            if (res != null) _reservations.Remove(res);
        }

        public void IssueBook(Book book, Reader reader)
        {
            var res = _reservations.FirstOrDefault(r => r.Book == book);

            if (res != null && res.Reader != reader && !res.IsExpired())
            {
                Console.WriteLine($"Книга \"{book.Title}\" зарезервирована за другим пользователем.");
                return;
            }

            if (_books.Contains(book))
            {
                reader.BorrowBook(book);
                _books.Remove(book);
                if (res != null) _reservations.Remove(res);
            }
            else
            {
                Console.WriteLine($"Книга \"{book.Title}\" недоступна.");
            }
        }

        public void ReturnBook(Book book)
        {
            _books.Add(book);
            Console.WriteLine($"Книга \"{book.Title}\" возвращена.");
        }
    }

    public abstract class Publication
    {
        public abstract void GetInfo();
    }

    public class BookPublication : Publication
    {
        private Book _book;
        public BookPublication(Book book) { _book = book; }
        public override void GetInfo() { _book.ShowInfo(); }
    }

    class Program
    {
        static void Main()
        {
            Library library = new Library();
            Textbook t1 = new Textbook("Математика 101", "Иванов", 2020, 300, "Математика");
            FictionBook f1 = new FictionBook("Война и мир", "Толстой", 1869, 1200, "Роман");

            library.AddBook(t1);
            library.AddBook(f1);
            
            Reader r1 = new Reader("Алексей", 1);
            Reader r2 = new Reader("Иван", 2);

            library.ReserveBook(f1, r1);
            library.IssueBook(f1, r2);
            library.IssueBook(f1, r1);

            Publication pub = new BookPublication(t1);
            pub.GetInfo();

            Console.ReadKey();
        }
    }
}







































Уровень 2
Добавьте возможность резервирования книг:
Создайте класс Резервирование﻿, который хранит ссылку на книгу, читателя, дату резервирования и срок действия.
В классе Library﻿ добавьте коллекцию резервов.
Реализуйте методы для создания резервирования книги и отмены.
При вызове выдачи книги учитывайте, что книгу нельзя выдать, если она зарезервирована другим читателем.
using System;
using System.Collections.Generic;
using System.Linq;

public class Reservation
{
    public Book Book { get; set; }
    public Reader Reader { get; set; }
    public DateTime ReservationDate { get; set; }
    public int ExpiryDays { get; set; }

    public Reservation(Book book, Reader reader, int expiryDays = 3)
    {
        Book = book;
        Reader = reader;
        ReservationDate = DateTime.Now;
        ExpiryDays = expiryDays;
    }

    public bool IsExpired() => DateTime.Now > ReservationDate.AddDays(ExpiryDays);
}

public class Library : ILibraryManagement
{
    private List<Book> _books = new List<Book>();
    private List<Reservation> _reservations = new List<Reservation>();

    public void AddBook(Book book) => _books.Add(book);

    public bool RemoveBook(Book book) => _books.Remove(book);

    public List<Book> SearchByAuthor(string author) => 
        _books.Where(b => b.Author == author).ToList();

    public void ListBooks()
    {
        foreach (var book in _books) book.ShowInfo();
    }

    public void ReserveBook(Book book, Reader reader)
    {
        if (_books.Contains(book))
        {
            _reservations.Add(new Reservation(book, reader));
            Console.WriteLine($"Книга \"{book.Title}\" зарезервирована для {reader.Name}.");
        }
    }

    public void CancelReservation(Book book)
    {
        var res = _reservations.FirstOrDefault(r => r.Book == book);
        if (res != null) _reservations.Remove(res);
    }

    public void IssueBook(Book book, Reader reader)
    {
        var res = _reservations.FirstOrDefault(r => r.Book == book);

        if (res != null && res.Reader != reader && !res.IsExpired())
        {
            Console.WriteLine($"Книга \"{book.Title}\" зарезервирована за другим пользователем.");
            return;
        }

        if (_books.Contains(book))
        {
            reader.BorrowBook(book);
            _books.Remove(book);
            if (res != null) _reservations.Remove(res);
        }
    }

    public void ReturnBook(Book book) => _books.Add(book);
}

class Program
{
    static void Main()
    {
        Library library = new Library();
        FictionBook f1 = new FictionBook("1984", "Оруэлл", 1949, 328, "Антиутопия");
        library.AddBook(f1);

        Reader r1 = new Reader("Алексей", 1);
        Reader r2 = new Reader("Иван", 2);

        library.ReserveBook(f1, r1);
        library.IssueBook(f1, r2);
        library.IssueBook(f1, r1);
        
        r1.ShowBorrowedBooks();
    }
}
