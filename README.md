# C-hw
hw notes

namespace ConsoleApplication2
{
    class Program
    {
        static void Main(string[] args)
        {
            Players[] table = new Players[3]
            {
                new Players
                {
                    NAME = "Bradley",
                    ID = 1,
                    ID_NAME = "pacprof",
                    CITY = "Chicago",
                    PAID_UP = true

                },
                new Players
                {
                    NAME = "Clayton",
                    ID = 2,
                    ID_NAME = "pokechamp",
                    CITY = "Chicago",
                    PAID_UP = false

                },
                new Players
                {
                    NAME = "Tina",
                    ID = 3,
                    ID_NAME = "pikachu",
                    CITY = "Chicago",
                    PAID_UP = true

                },

            };

            Ownership[] table3 = new Ownership[2]
            {
                new Ownership
                {
                    PLAYER_ID = 1,
                    POKEMON_ID = 1,
                    LEVEL = 11,
                    NUMBER_OWNED = 1
                },
                new Ownership
                {
                    PLAYER_ID = 1,
                    POKEMON_ID = 5,
                    LEVEL = 9,
                    NUMBER_OWNED = 2
                },


            };

            foreach (var entry in table)
            {
                Console.Write("{0}", entry);
                Console.WriteLine();
            }

            // enter city name, get usernames associated with city
            Console.Write("Enter city name: ");
            string cityName = Console.ReadLine();

            var qryCity = from player in table
                          where player.CITY.ToLower() == cityName.ToLower()
                          orderby player.PAID_UP 
                          select new { player.ID_NAME, player.PAID_UP };

            Console.WriteLine();
            string nickname = "--User Name--";
            string paidStatus = "--Paid Status--";
            Console.WriteLine("Users from {0}", cityName.ToUpper());
            Console.Write("{0,-20}{1}\n", nickname, paidStatus);
            foreach (var element in qryCity)
            {
                Console.Write("{0,11} | {1,19} |", element.ID_NAME, element.PAID_UP);
                Console.WriteLine();
            }

            Console.WriteLine("Player ID: ");
            int key = Convert.ToInt32(Console.ReadLine());
            // input player ID or nickname
            var innerJoinQuery =
                    from player in table
                    join owner in table3 on player.ID equals owner.PLAYER_ID
                    where owner.PLAYER_ID == key
                    select new { owner.POKEMON_ID };
            
            foreach (var element in innerJoinQuery)
            {
                Console.Write("{0}", element);
                Console.WriteLine();
            }

            Console.ReadKey();
        }
    }
}


