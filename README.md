using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace asd
{
    internal class Program
    {
        static int num;

        static void Main(string[] args)
        {
            Dictionary<int, string> myDictionary = new Dictionary<int, string>();

        Menu:
            Console.WriteLine("\n--------------------Menu-------------------");
            Console.Write("What would you want to do? ");

            Console.WriteLine("\n\n 1.Caculate water bill \n 2.Add the customer's bill \n 3.Find the customer's bill  \n 4.Show and sort customer's information \n 5.Exit");
            Console.Write("\nEnter your option (1-5): ");
            double ChooseOption = Convert.ToInt32(Console.ReadLine());
            switch (ChooseOption)
            {
                case 1:
                    CaculateWaterBill();
                    goto Menu;
                case 2:
                    goto inputValue;
                case 3:
                    goto FindCustomer;
                case 4:
                    Console.WriteLine("--------------------List of customer--------------------");
                    ShowAndSortCustomerInformation(myDictionary);
                    goto Menu;
                case 5:
                    Console.WriteLine("Exiting");
                    Environment.Exit(0);

                    break;

                default:
                    Console.WriteLine("invaild value");
                    Console.ReadLine();
                    goto Menu;
            }

        inputValue:
            Console.WriteLine("--------------------Add the customer's bill--------------------");
            String notice = " ";

            while (true)
            {
                Console.Write("\nEnter bill (VND): ");
                string bill = Console.ReadLine();


                if (!int.TryParse(bill, out int key))
                {
                    Console.WriteLine("Invalid value");
                    continue;
                }

                Console.Write("Enter customer name: ");
                string name = Console.ReadLine();
                myDictionary[key] = name;

                Console.Write("Do you want to continute (y/n): ");

                notice = Console.ReadLine();
                if (notice.ToLower() == "n")
                    goto Menu;
            }
        FindCustomer:
            string find = " ";
            Console.WriteLine("--------------------SearchCustomer--------------------");

            while (true)
            {
                Console.Write("\nEnter customer name to find: ");
                string nameToFind = Console.ReadLine();
                FindCustomer(myDictionary, nameToFind);
                Console.ReadLine();
                Console.Write("Do you want to continute (y/n): ");
                find = Console.ReadLine();
                if (find.ToLower() == "n")
                {
                    Console.WriteLine("Back to the menu.....");
                    goto Menu;

                }

            }
        }
        static void CaculateWaterBill()
        {
            String cont = " ";

            while (true)
            {
                
                    Console.Write("\nLast month’s water meter readings (m3):");
                    double a = Convert.ToInt32(Console.ReadLine());

                    Console.Write("This month’s water meter readings (m3):");
                    double b = Convert.ToInt32(Console.ReadLine());

                    Console.WriteLine($"\nWater Comsumed: {b - a} " + "m3");

                    double c = b - a;
                    if (c < 0)
                    {
                        Console.WriteLine("Invaild value");
                        break;
                    }
                Type:
                    Console.WriteLine("\nType of customer:\n 1.Household customer \n 2.Administrative agency, public services \n 3.Production units \n 4.Business services");
                    Console.Write("\nSelect type of customer: ");
                    double caculator = Convert.ToInt32(Console.ReadLine());




                    switch (caculator)
                    {
                        case 1:
                            if (c < 10)
                            {
                                Console.WriteLine($"\nVAT : {(c * 5973) * 10 / 100} VND \nTotal water bill : {(c * 5973) + (c * 5973) * 10 / 100} VND");
                                Console.ReadLine();
                            }
                            else if (c >= 10 && c < 20)
                            {
                                Console.WriteLine($"\nVAT:{(c * 7052) * 10 / 100} VND \nTotal water bill : {(c * 7052) + (c * 7052) * 10 / 100} VND");
                                Console.ReadLine();

                            }
                            else if (c >= 20 && c < 30)
                            {
                                Console.WriteLine($"\nVAT:{(c * 8699) * 10 / 100} VND \nTotal water bill : {(c * 8699) + (c * 8699) * 10 / 100} VND");
                                Console.ReadLine();

                            }
                            else if (c >= 30)
                            {
                                Console.WriteLine($"\nVAT: {(c * 15929) * 10 / 100} VND \nTotal water bill : {(c * 15929) + (c * 15929) * 10 / 100} VND");
                                Console.ReadLine();

                            }
                            else
                            {
                                Console.WriteLine("Invaild value");
                            }
                            break;
                        case 2:
                            Console.WriteLine($"\nVAT: {(c * 9955) * 10 / 100} VND \nTotal water bill : {(c * 9955) + (c * 9955) * 10 / 100} VND");
                            Console.ReadLine();

                            break;
                        case 3:
                            Console.WriteLine($"\nVAT: {(c * 11615) * 10 / 100} VND \nTotal water bill : {(c * 11615) + (c * 11615) * 10 / 100} VND");
                            Console.ReadLine();

                            break;
                        case 4:
                            Console.WriteLine($"\nVAT:  {(c * 22068) * 10 / 100} VND  \nTotal water bill : {(c * 22068) + (c * 22068) * 10 / 100} VND");
                            Console.ReadLine();

                            break;
                        default:
                            Console.WriteLine("Choose 1 to 4 please! ");
                            Console.ReadLine();
                            goto Type;
                    }
                    Console.Write("Do you want to continute (y/n): ");
                    cont = Console.ReadLine();
                if (cont.ToLower() == "n")
                {
                    Console.WriteLine("Back to the menu.....");
                    break;
                }

                
            }
        }

        static void FindCustomer(Dictionary<int, string> dictionary, string name)
        {
            var foundCustomers = new List<int>();

            foreach (var kvp in dictionary)
            {
                if (kvp.Value.Equals(name, StringComparison.OrdinalIgnoreCase))
                {
                    foundCustomers.Add(kvp.Key);
                }
            }

            if (foundCustomers.Count > 0)
            {
                Console.WriteLine($"Customer(s) found with name :{name}");
                Console.WriteLine("Bill:" + string.Join(", ", foundCustomers ) + " VND");
            }
            else
            {
                Console.WriteLine($"Customer with name '{name}' not found.");
            }


        }
        static void ShowAndSortCustomerInformation(Dictionary<int, string> dictionary)
        {
            String sort = " ";


            foreach (var kvp in dictionary)
            {
                Console.WriteLine("\nCustomer name: " + kvp.Value + " \nBill: " + kvp.Key + " VND");
            }
            Console.Write("Do you want to sort (y/n): ");
            sort = Console.ReadLine();
            if (sort.ToLower() == "y")
            {
                var sortedDictionary = dictionary.OrderBy(pair => pair.Key).ToDictionary(pair => pair.Key, pair => pair.Value);
                Console.WriteLine("\nSorted Customer Information:");
                ShowAndSortCustomerInformation(sortedDictionary);
            }
            else
            {
                Console.WriteLine("Back to the menu....");
            }
        }

    }


}
