# Csharp_lab03
## Цели работы:
  1. Научиться синтаксису и принципам перегрузки операторов языка C#.

## Задание №1
Создайте структуру Vector с тремя полями x, y и z. 
Для созданной структуры переопределите операторы сложения векторов, умножения векторов, умножения вектора на число, а также логические операторы. Для логических операторов используйте сравнение по длине от начала координат.

## Задание №2
Создайте класс Car со свойствами Name, Engine, MaxSpeed. Переопределите оператор ToString() таким образом, чтобы он возвращал название машины(Name). Реализуйте возможность сравнения объектов Car, реализовав интерфейс IEquatable<Car>. 
Создайте класс CarsCatalog, содержащий коллекцию машин – элементов типа Car и переопределите для него индексатор таким образом, чтобы он возвращал строку с названием машины и типом двигателя.

## Задание №3
Создайте базовый класс Currency со свойством Value. Создайте 3 производных от Currency класса – CurrencyUSD, CurrencyEUR и CurrencyRUB со свойствами, соответствующими обменному курсу. В каждом из производных классов переопределите операторы преобразования типов таким образом, чтобы можно было явно или неявно преобразовать одну валюту в другую по курсу, заданному пользователем при запуске программы.

## Код задания № 1
    using System;
    
    struct Vector
    {
        public double x;
        public double y;
        public double z;
    
        public Vector(double x, double y, double z)
        {
            this.x = x;
            this.y = y;
            this.z = z;
        }
    
        // Переопределение оператора сложения векторов
        public static Vector operator +(Vector v1, Vector v2)
        {
            return new Vector(v1.x + v2.x, v1.y + v2.y, v1.z + v2.z);
        }
    
        // Переопределение оператора умножения векторов (скалярное произведение)
        public static double operator *(Vector v1, Vector v2)
        {
            return v1.x * v2.x + v1.y * v2.y + v1.z * v2.z;
        }
    
        // Переопределение оператора умножения вектора на число
        public static Vector operator *(Vector v, double scalar)
        {
            return new Vector(v.x * scalar, v.y * scalar, v.z * scalar);
        }
    
        // Переопределение оператора умножения числа на вектор
        public static Vector operator *(double scalar, Vector v)
        {
            return new Vector(v.x * scalar, v.y * scalar, v.z * scalar);
        }
    
        // Вычисление длины вектора от начала координат
        public double Length()
        {
            return Math.Sqrt(x * x + y * y + z * z);
        }
    
        // Переопределение оператора "равно" для сравнения длины векторов
        public static bool operator ==(Vector v1, Vector v2)
        {
            return v1.Length() == v2.Length();
        }
    
        // Переопределение оператора "не равно" для сравнения длины векторов
        public static bool operator !=(Vector v1, Vector v2)
        {
            return !(v1 == v2);
        }
    
        // Переопределение оператора "меньше" для сравнения длины векторов
        public static bool operator <(Vector v1, Vector v2)
        {
            return v1.Length() < v2.Length();
        }
    
        // Переопределение оператора "больше" для сравнения длины векторов
        public static bool operator >(Vector v1, Vector v2)
        {
            return v1.Length() > v2.Length();
        }
    
        // Переопределение оператора "меньше или равно" для сравнения длины векторов
        public static bool operator <=(Vector v1, Vector v2)
        {
            return v1.Length() <= v2.Length();
        }
    
        // Переопределение оператора "больше или равно" для сравнения длины векторов
        public static bool operator >=(Vector v1, Vector v2)
        {
            return v1.Length() >= v2.Length();
        }
    
        public override string ToString()
        {
            return $"Vector({x}, {y}, {z})";
        }
    }
    
    
    class Program
    {
        static void Main(string[] args)
        {
            // Создание двух векторов
            Vector v1 = new Vector(3, 4, 0);
            Vector v2 = new Vector(1, 2, 2);
    
            // Проверка операции сложения
            Vector sum = v1 + v2;
            Console.WriteLine($"Сложение: {v1} + {v2} = {sum}");
    
            // Проверка скалярного произведения
            double dotProduct = v1 * v2;
            Console.WriteLine($"Скалярное произведение: {v1} * {v2} = {dotProduct}");
    
            // Проверка умножения вектора на число
            double scalar = 2;
            Vector scaledVector = v1 * scalar;
            Console.WriteLine($"Умножение вектора на число: {v1} * {scalar} = {scaledVector}");
    
            // Проверка умножения числа на вектор
            Vector scaledVector2 = scalar * v2;
            Console.WriteLine($"Умножение числа на вектор: {scalar} * {v2} = {scaledVector2}");
    
            // Проверка логических операторов
            Console.WriteLine($"Длина вектора {v1} = {v1.Length()}");
            Console.WriteLine($"Длина вектора {v2} = {v2.Length()}");
    
            Console.WriteLine($"{v1} == {v2}: {v1 == v2}");
            Console.WriteLine($"{v1} != {v2}: {v1 != v2}");
            Console.WriteLine($"{v1} > {v2}: {v1 > v2}");
            Console.WriteLine($"{v1} < {v2}: {v1 < v2}");
            Console.WriteLine($"{v1} >= {v2}: {v1 >= v2}");
            Console.WriteLine($"{v1} <= {v2}: {v1 <= v2}");
        }
    }
## Код задания № 2
    using System;
    using System.Collections.Generic; // Используем чтобы создать коллекцию List<Car>
    
    // Класс Car, реализующий интерфейс IEquatable<Car>
    public class Car : IEquatable<Car>
    {
        // Свойства Name, Engine, MaxSpeed
        public string Name { get; set; }
        public string Engine { get; set; }
        public int MaxSpeed { get; set; }
    
        // Конструктор для инициализации свойств
        public Car(string name, string engine, int maxSpeed)
        {
            Name = name;
            Engine = engine;
            MaxSpeed = maxSpeed;
        }
    
        // Переопределение метода ToString()
        public override string ToString()
        {
            return Name;
        }
    
        // Реализация интерфейса IEquatable<Car>
        public bool Equals(Car other)
        {
            if (other == null) return false;
            return this.Name == other.Name && this.Engine == other.Engine && this.MaxSpeed == other.MaxSpeed;
        }
    
        // Переопределение метода Equals для класса Object (чтобы сравнивать не по ссылке в памяти, а по значениям)
        public override bool Equals(object obj)
        {
            if (obj == null || !(obj is Car)) return false;
            return Equals((Car)obj);
        }
    }
    
    // Класс CarsCatalog с коллекцией машин и индексатором
    public class CarsCatalog
    {
        // Коллекция машин
        private List<Car> cars = new List<Car>();
    
        // Метод для добавления машин в каталог
        public void AddCar(Car car)
        {
            cars.Add(car);
        }
    
        // Индексатор, возвращающий строку с названием машины и типом двигателя
        public string this[int index]
        {
            get
            {
                if (index < 0 || index >= cars.Count)
                    throw new IndexOutOfRangeException("Invalid index");
    
                Car car = cars[index];
                return $"Name: {car.Name}, Engine: {car.Engine}";
            }
        }
    }
    
    // Пример использования
    class Program
    {
        static void Main()
        {
            // Создание машин
            Car car1 = new Car("Ferrari", "V8", 350);
            Car car2 = new Car("BMW", "V12", 370);
    
            // Создание каталога машин и добавление в него машин
            CarsCatalog catalog = new CarsCatalog();
            catalog.AddCar(car1);
            catalog.AddCar(car2);
    
            // Использование индексатора для получения информации о машине
            Console.WriteLine(catalog[0]);
            Console.WriteLine(catalog[1]);
    
            // Сравнение объектов Car
            Console.WriteLine($"car1 = car2: {car1.Equals(car2)}");
        }
    }
## Код задания № 3
    using System;
    
    // Базовый класс для представления валюты
    public class Currency
    {
        // Свойство, представляющее значение валюты
        public double Value { get; set; }
    
        // Конструктор, инициализирующий значение валюты
        public Currency(double value)
        {
            Value = value;
        }
    
        // Переопределение ToString для отображения значения валюты
        public override string ToString() => Value.ToString("F2"); // Форматирование до 2 знаков после запятой
    }
    
    // Класс для представления валюты USD
    public class CurrencyUSD : Currency
    {
        public CurrencyUSD(double value) : base(value) { }
    
        // Явное преобразование USD в EUR
        public static explicit operator CurrencyEUR(CurrencyUSD usd)
        {
            double exchangeRate = CurrencyExchangeRates.ExchangeRateUSDToEUR;
            return new CurrencyEUR(usd.Value * exchangeRate);
        }
    
        // Неявное преобразование USD в RUB
        public static implicit operator CurrencyRUB(CurrencyUSD usd)
        {
            double exchangeRate = CurrencyExchangeRates.ExchangeRateUSDToRUB;
            return new CurrencyRUB(usd.Value * exchangeRate);
        }
    }
    
    // Класс для представления валюты EUR
    public class CurrencyEUR : Currency
    {
        public CurrencyEUR(double value) : base(value) { }
    
        // Явное преобразование EUR в USD
        public static explicit operator CurrencyUSD(CurrencyEUR eur)
        {
            double exchangeRate = CurrencyExchangeRates.ExchangeRateEURToUSD;
            return new CurrencyUSD(eur.Value * exchangeRate);
        }
    
        // Неявное преобразование EUR в RUB
        public static implicit operator CurrencyRUB(CurrencyEUR eur)
        {
            double exchangeRate = CurrencyExchangeRates.ExchangeRateEURToRUB;
            return new CurrencyRUB(eur.Value * exchangeRate);
        }
    }
    
    // Класс для представления валюты RUB
    public class CurrencyRUB : Currency
    {
        public CurrencyRUB(double value) : base(value) { }
    
        // Явное преобразование RUB в USD
        public static explicit operator CurrencyUSD(CurrencyRUB rub)
        {
            double exchangeRate = CurrencyExchangeRates.ExchangeRateRUBToUSD;
            return new CurrencyUSD(rub.Value * exchangeRate);
        }
    
        // Неявное преобразование RUB в EUR
        public static implicit operator CurrencyEUR(CurrencyRUB rub)
        {
            double exchangeRate = CurrencyExchangeRates.ExchangeRateRUBToEUR;
            return new CurrencyEUR(rub.Value * exchangeRate);
        }
    }
    
    // Класс для хранения обменных курсов
    public static class CurrencyExchangeRates
    {
        public static double ExchangeRateUSDToEUR { get; set; }
        public static double ExchangeRateUSDToRUB { get; set; }
        public static double ExchangeRateEURToUSD { get; set; }
        public static double ExchangeRateEURToRUB { get; set; }
        public static double ExchangeRateRUBToUSD { get; set; }
        public static double ExchangeRateRUBToEUR { get; set; }
    }
    
    // Основной класс программы
    class Program
    {
        static void Main()
        {
            // Запрос обменных курсов у пользователя
            Console.WriteLine("Вводите курс через ',' например: 0,86");
            Console.WriteLine("Введите курс USD к EUR:");
            CurrencyExchangeRates.ExchangeRateUSDToEUR = Convert.ToDouble(Console.ReadLine());
    
            Console.WriteLine("Введите курс USD к RUB:");
            CurrencyExchangeRates.ExchangeRateUSDToRUB = Convert.ToDouble(Console.ReadLine());
    
            Console.WriteLine("Введите курс EUR к USD:");
            CurrencyExchangeRates.ExchangeRateEURToUSD = Convert.ToDouble(Console.ReadLine());
    
            Console.WriteLine("Введите курс EUR к RUB:");
            CurrencyExchangeRates.ExchangeRateEURToRUB = Convert.ToDouble(Console.ReadLine());
    
            Console.WriteLine("Введите курс RUB к USD:");
            CurrencyExchangeRates.ExchangeRateRUBToUSD = Convert.ToDouble(Console.ReadLine());
    
            Console.WriteLine("Введите курс RUB к EUR:");
            CurrencyExchangeRates.ExchangeRateRUBToEUR = Convert.ToDouble(Console.ReadLine());
    
            // Примеры преобразования валют
            CurrencyUSD usd = new CurrencyUSD(100);
            Console.WriteLine($"Явное преобразование 100 USD в EUR: {(CurrencyEUR)(usd)}"); // Явное преобразование
            Console.WriteLine($"Неявное преобразование 100 USD в RUB: {(usd)}"); // Неявное преобразование
    
            CurrencyEUR eur = new CurrencyEUR(100);
            Console.WriteLine($"Явное преобразование 100 EUR в USD: {(CurrencyUSD)(eur)}"); // Явное преобразование
            Console.WriteLine($"Неявное преобразование 100 EUR в RUB: {(eur)}"); // Неявное преобразование
    
            CurrencyRUB rub = new CurrencyRUB(100);
            Console.WriteLine($"Явное преобразование 100 RUB в USD: {(CurrencyUSD)(rub)}"); // Явное преобразование
            Console.WriteLine($"Неявное преобразование 100 RUB в EUR: {(rub)}"); // Неявное преобразование
        }
    }
C# lab03
