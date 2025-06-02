# Portfolio-Assignment-Submission
    class Program
{
    
    static List<InsuranceQuote> quotes = new List<InsuranceQuote>();
    static int nextId = 1;

    static void Main(string[] args)
    {
        bool running = true;

        while (running)
        {
            Console.WriteLine("Car Insurance Quote System");
            Console.WriteLine("1. Get a Quote");
            Console.WriteLine("2. Admin - View All Quotes");
            Console.WriteLine("3. Exit");
            Console.Write("Choose an option: ");
            string choice = Console.ReadLine();

            Console.Clear();

            switch (choice)
            {
                case "1":
                    CreateQuote();
                    break;
                case "2":
                    ShowAdminPage();
                    break;
                case "3":
                    running = false;
                    break;
                default:
                    Console.WriteLine("Invalid option.");
                    break;
            }

            Console.WriteLine("");
            Console.ReadLine();
            Console.Clear();
        }
    }

    static void CreateQuote()
    {
        var quote = new InsuranceQuote();
        quote.Id = nextId++;

        Console.Write("Full Name: ");
        quote.FullName = Console.ReadLine();

        Console.Write("Age: ");
        quote.Age = int.Parse(Console.ReadLine());

        Console.Write("Car Make: ");
        quote.CarMake = Console.ReadLine();

        Console.Write("Car Year: ");
        quote.CarYear = int.Parse(Console.ReadLine());

        Console.Write("Any Accidents in Last 5 Years? (yes/no): ");
        string accidentInput = Console.ReadLine().ToLower();
        quote.HasAccidents = (accidentInput == "yes");

        
        decimal basePrice = 500m;

        if (quote.Age < 25) basePrice += 100;
        if (quote.CarYear < 2015) basePrice += 50;
        if (quote.CarMake.ToLower() == "bmw") basePrice += 75;
        if (quote.HasAccidents) basePrice += 100;

        quote.QuoteAmount = basePrice;

        quotes.Add(quote);

        Console.WriteLine($"\nThank you, {quote.FullName}!");
        Console.WriteLine($"Your estimated insurance quote is: ${quote.QuoteAmount}");
    }

    static void ShowAdminPage()
    {
        Console.WriteLine("Issued Insurance Quotes:");
        Console.WriteLine("--------------------------------------------------");
        foreach (var q in quotes)
        {
            Console.WriteLine($"ID: {q.Id} | Name: {q.FullName} | Car: {q.CarYear} {q.CarMake} | Quote: ${q.QuoteAmount}");
        }

        if (quotes.Count == 0)
        {
            Console.WriteLine("No quotes issued yet.");
        }
    }
}
