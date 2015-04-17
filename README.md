# CSharpTimer
A timer/alarm made using C#




namespace Reduced_Timer
{
    class Program
    {
        public static string _or;
        public static Thread playNoises = new Thread(PlayNoises);

        static void Main(string[] args)
        {
            //This is a copy of my original timer program. It uses a thread so that sound will alert the user once the timer goes off, and the timer will keep going off until the user stops it.
            Console.Title = "Program started at: " + DateTime.Now;
            Console.WriteLine("Hours, minutes, of seconds?");
            _or = Console.ReadLine();

            if (_or == "seconds")
            {
                Timer(1000);
            }
            else if (_or == "minutes")
            {
                Timer(60000);
            }
            else if (_or == "Hours")
            {
                Timer(360000);
            }
            else
            {
                Console.WriteLine("Sorry, we couldn't understand your measurement of time!");
            }
        } // end of public void

        public static void Timer (int x)
        {
            Console.WriteLine("You chose " + _or + ", please tell us how many " + _or);
            var many2 = Console.ReadLine();
            Console.Title = "Timer started at: " + DateTime.Now;
            for (int m2 = Convert.ToInt32(many2); m2 > 0; m2--) // All that these FOR loops do is delay the program for the set amount of time.
            {
                Thread.Sleep(x); // again, sleeps the program till it finishes.
            }

            Console.WriteLine("It has been " + many2 + " seconds");
            playNoises.Start(); // This function does the same thing as our previous program, but it keeps going while it waits for an answer.
            var timeAfter = DateTime.Now;

            Console.Read();
            playNoises.Abort();
            Console.WriteLine("The timer went off at: " + timeAfter);
            Console.WriteLine("Timer stopped at: " + DateTime.Now);

            Console.ReadKey();
        } // end of the Timer function

        public static void PlayNoises() //this is our PlayNoises function, it replaces the ONE system sound and makes it loop until the user stops it!
        {
            while (true)
            {
                SystemSounds.Asterisk.Play();
                Thread.Sleep(2500);
            }
        } // end of the PlayNoises void funtion.

    }
}
