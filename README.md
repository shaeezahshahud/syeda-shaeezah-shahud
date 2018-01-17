# syeda-shaeezah-shahud
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace pigeonhole
{
    class Filing
    {
        string mydocpath = "C:\\Users\\farhan\\Desktop\\pigeon.txt";
        public void Writer(int[] Array)
        {
            using (StreamWriter SW = new StreamWriter(mydocpath))
            {
                for (int i = 0; i < Array.Length; i++)
                {
                    SW.WriteLine(Array[i]);
                }
            }
        }
        public int Getlength()
        {
            int Count = 0;
            try
            {
                using (StreamReader SR = new StreamReader(mydocpath))
                {
                    string line;
                    while ((line = SR.ReadLine()) != null)
                    {
                        Count++;
                    }
                }
            }
            catch (Exception e)
            {
                Console.WriteLine("Error 404! File Not Found");
                Console.WriteLine(e.Message);
            }
            return Count;
        }
        public int[] Reader(int Len)
        {
            int[] Arr = new int[Len];
            try
            {
                using (StreamReader SR = new StreamReader(mydocpath))
                {
                    for (int i = 0; i < Len; i++)
                    {
                        Arr[i] = Convert.ToInt16(SR.ReadLine());
                        Console.WriteLine("  Array[{0}] : {1}", i, Arr[i]);
                    }
                }
            }
            catch (Exception e)
            {
                Console.WriteLine("Error 404! File Not Found");
                Console.WriteLine(e.Message);
            }
            return Arr;
        }
    }
    class Pigeon_hole
    {
        public int[] pigeonhole(int[] arr)
        {
            int min = arr[0];
            int max = arr[0];
            for (int i = 0; i < arr.Length; i++)
            {
                if (arr[i] > max)
                {
                    max = arr[i];
                }
                if (arr[i] < min)
                {
                    min = arr[i];
                }
            }
            int range = max - min + 1;
            int[] phole = new int[range];
            for (int j = 0; j < arr.Length; j++)
            {
                phole[arr[j] - min]++;
            }
            int index = 0;
            for (int k = 0; k < range; k++)
            {
                while (phole[k]-- > 0)
                    arr[index++] = k + min;
            }
            return arr;
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("===============================================================================================");
            Console.WriteLine("                                    PigoenHole Sort                                            ");
            Console.WriteLine("===============================================================================================");
            Filing F = new Filing();
            int Len = F.Getlength();
            Console.WriteLine("  Length of Array is : " + Len);
            Console.WriteLine("\n  Before Sorting: ");
            int[] arr = F.Reader(Len);
            Pigeon_hole ph = new Pigeon_hole();
            Console.WriteLine("\n\n  After Sorting: ");
            arr = ph.pigeonhole(arr);
            for (int i = 0; i < Len; i++)
            {
                Console.WriteLine("  Array[{0}] : {1}", i, arr[i]);
            }
            F.Writer(arr);
            Console.ReadLine();
        }
    }
}
