# Leo-D.-Angelo-Mekonnen_ST10148045_PROG6221_ICE-Task-1

using System;

namespace ICE_Task_1
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Welcome to the script marking allocation application!");
            Console.WriteLine("Please enter the following inputs:");

            // Get the total number of scripts
            int totalScripts;
            do
            {
                Console.Write("Total number of scripts to be marked: ");
            } while (!int.TryParse(Console.ReadLine(), out totalScripts) || totalScripts <= 0);

            // Get the number of questions in the test
            int numQuestions;
            do
            {
                Console.Write("Number of questions in the test (1-10): ");
            } while (!int.TryParse(Console.ReadLine(), out numQuestions) || numQuestions < 1 || numQuestions > 10);

            // Get the subtotals for each question
            int[] subtotals = new int[numQuestions];
            for (int i = 0; i < numQuestions; i++)
            {
                do
                {
                    Console.Write($"Subtotal for question {i + 1}: ");
                } while (!int.TryParse(Console.ReadLine(), out subtotals[i]) || subtotals[i] <= 0);
            }

            // Get the number of lecturers
            int numLecturers;
            do
            {
                Console.Write("Number of lecturers who will mark the scripts: ");
            } while (!int.TryParse(Console.ReadLine(), out numLecturers) || numLecturers <= 0);

            // Calculate the number of scripts each lecturer will mark
            int[] scriptsPerLecturer = new int[numLecturers];
            int scriptsRemaining = totalScripts;
            for (int i = 0; i < numLecturers; i++)
            {
                scriptsPerLecturer[i] = scriptsRemaining / (numLecturers - i);
                scriptsRemaining -= scriptsPerLecturer[i];
            }

            // Calculate the estimated time for each lecturer to finish marking
            Console.WriteLine("\nAllocation Results:");
            for (int i = 0; i < numLecturers; i++)
            {
                int numTicks = scriptsPerLecturer[i] * numQuestions;
                int minutes = numTicks * 2 / 60;
                int seconds = numTicks * 2 % 60;
                if (seconds >= 30) minutes++;
                Console.WriteLine($"Lecturer {i + 1}: {scriptsPerLecturer[i]} scripts, {minutes}h {(minutes > 0 ? minutes % 60 : 0)}m");
            }

            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
