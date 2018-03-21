using System;
using System.Collections.Generic;

namespace BinarySearch
{
    class Searcher
    {
        static void Main(string[] args)
        {

            Searcher searcher = new Searcher();
            System.Random r = new Random(searcher.GetHashCode());
            int length = 1000000;

            Console.WriteLine("Go?");
            Console.ReadKey();

            Console.ForegroundColor = ConsoleColor.Green;


            List<int> test = new List<int>();
            for(int i = 0; i < length; i++)
            {
                test.Add(i);
                //Console.Write(GetBin(t));
            }

            test = Shuffle(test, r);
            Console.WriteLine("List created");
            Console.ReadKey();

            test = searcher.RadixSort(test);
            Console.WriteLine("List sorted (length "+length+"), press any key to print list");
            Console.ReadKey();

           
            PrintArray(test);
            //Console.WriteLine("Enter search term: ");
            //int needle = int.Parse(Console.ReadLine());

            //int index = searcher.BinarySearch(test.ToArray(), needle);

            //List<int> indexes = new List<int>();
            //indexes.Add(index);

            //Console.WriteLine((index == -1) ? "Not in array" : "At index position: "); PrintArray(searcher.Thing(test.ToArray(), needle, index));
            Console.ReadKey();
        }

        public static List<T> Shuffle<T>(List<T> list, Random rng)
        {
            int n = list.Count;
            while (n > 1)
            {
                n--;
                int k = rng.Next(n + 1);
                T value = list[k];
                list[k] = list[n];
                list[n] = value;
            }
            return list;
        }

        List<int> Thing(int[] array, int needle, int startIndex, bool left = true)
        {
            List<int> t = new List<int>();
            Console.WriteLine(startIndex);
            if (left && startIndex >= 0)
            {
                if (array[startIndex] == needle)
                {
                    t.AddRange(Thing(array, needle, startIndex - 1));
                }
            }

            else if (startIndex < array.Length && startIndex >= 0
                )
            {
                if (array[startIndex] == needle)
                {
                    left = false;
                    t.AddRange(Thing(array, needle, startIndex + 1, left));
                }
            }

            return t;
        }

        int BinarySearch(int[] array, int needle)
        {
            Console.WriteLine("bik");
            return BinarySearch(array, needle, 0, array.Length);
        }

        int BinarySearch(int[] array, int needle, int start, int end)
        {
            int mid = (start + end) / 2;

            if (start >= end)
            {
                return -1;
            }

            if (array[mid] == needle)
            {
                return mid;
            }
            else if (array[mid] > needle)
            {
                return BinarySearch(array, needle, start, mid - 1);
            }
            else
            {
                return BinarySearch(array, needle, mid + 1, end);
            }
        }

        int[] SplitArray(int[] arr, int start, int end)
        {
            int counter = 0;
            int[] result = new int[end - start];
            for (int i = start; i < end; i++)
            {
                result[counter] = arr[i];
                counter++;
            }

            return result;
        }


        static void PrintArray(List<int> result, string extraBefore = "", string extraAfter = "")
        {
            Console.Write(extraBefore);
            foreach (int item in result)
            {
                Console.Write(item + " ");
            }
            Console.Write(extraAfter);
        }

        static void PrintArray(int[] result, string extraBefore = "", string extraAfter = "")
        {
            Console.Write(extraBefore);
            foreach (int item in result)
            {
                Console.Write(item+ " ");
            }
            Console.Write(extraAfter);
        }

        static void PrintBinArray(int[] result, string extraBefore = "", string extraAfter = "")
        {
            Console.Write(extraBefore);
            foreach (int item in result)
            {
                Console.Write(GetBin(item) + " ");
            }
            Console.Write(extraAfter);
        }

        static void PrintBinArray(List<int> result, string extraBefore = "", string extraAfter = "")
        {
            Console.Write(extraBefore);
            foreach (int item in result)
            {
                Console.Write(GetBin(item) + " ");
            }
            Console.Write(extraAfter);
        }

        static string GetBin(int den)
        {
            // Final variables
            string binaryString = "";
            int tempDecimal = den;

            // Loop controls repeated division
            while (tempDecimal >= 1)
            {
                binaryString = binaryString + (tempDecimal % 2).ToString();
                tempDecimal /= 2;
            }

            return binaryString;
        }
            

        List<int> MergeSort(List<int> array)
        {
            for (int i = 0; i < array.Count; i++)
            {
                if (array.Count <= 1)
                    return array;

                List<int> left = ArrayUntil(array, 0, array.Count / 2);
                List<int> right = ArrayUntil(array, array.Count / 2, array.Count);

                //PrintArray(left, "Left: ", "\n");
                //PrintArray(right, "Right: ", "\n");

                left = MergeSort(left);
                right = MergeSort(right);

                return Merge(left, right);
            }

            return null;
        }

        List<int> Merge(List<int> left, List<int> right)
        {
            List<int> result = new List<int>();
            while (left.Count > 0 && right.Count > 0)
            {
                if (left[0] < right[0])
                {
                    result.Add(left[0]);
                    left.RemoveAt(0);
                }
                else
                {
                    result.Add(right[0]);
                    right.RemoveAt(0);
                }
            }

            if (left.Count > 0)
            {
                result.AddRange(left);
            }

            if (right.Count > 0)
            {
                result.AddRange(right);
            }



            return result;
        }

        List<int> ArrayUntil(List<int> array, int startIndex, int lastIndex)
        {
            List<int> newArr = new List<int>();
            for (int i = startIndex; i < lastIndex; i++)
            {
                newArr.Add(array[i]);
            }

            return newArr;
        }

        List<int> RadixSort(List<int> array, int bese = 2)
        {
            int maxVal = GetMaxValue(array);
            int it = 0;

            while(Math.Pow(bese, it) <= maxVal)
            {
                array = BucketToList(ListToBuckets(array, bese, it));
                it++;
            }

            return array;
        }

        int GetMaxValue(List<int> array)
        {
            int max = array[0];
            foreach(int n in array)
            {
                if (n > max)
                {
                    max = n;
                }
            }
            return max;
        }

        List<List<int>> ListToBuckets(List<int> array, int bese, int iteration)
        {
            List<List<int>> buckets = new List<List<int>>();
            for(int i = 0; i< array.Count; i++)
            {
                buckets.Add(new List<int>());
            }

            foreach(int number in array)
            {
                // Isolate the base-digit from the number
                int digit = (int)(number / (Math.Pow(bese, iteration))) % bese;
                // Drop into correct bucket
                buckets[digit].Add(number);
            }
            return buckets;
        }

        List<int> BucketToList(List<List<int>> buckets)
        {
            List<int> numbers = new List<int>();
            foreach (List<int> bucket in buckets)
            {
                numbers.AddRange(bucket);
            }
            return numbers;
        }
    }
}
