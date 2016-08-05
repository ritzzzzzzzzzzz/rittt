using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.SqlClient;
using System.Data;
namespace minefirst
{
    public class empdb
    {
        public List<emp1> viewemp()
        {
            string connectionstring = @"Data Source=inchnilpdb02\mssqlserver1;Initial Catalog=CHN12_MMS73_TEST;User ID=mms73user;Password=mms73user"; 
            SqlConnection con = new SqlConnection(connectionstring);
            con.Open(); SqlCommand cmd = new SqlCommand(); 
            cmd.CommandType = CommandType.StoredProcedure;
            cmd.CommandText = "sp_view1";
            cmd.Connection = con; 
            SqlDataReader dr = cmd.ExecuteReader();
            List<emp1> listt = new List<emp1>();
          //  cmd.Parameters.AddWithValue("@id", listt[0].id);
            while (dr.Read())
            {
                int id = Convert.ToInt32(dr["id"]);
                string name = Console.ReadLine();
                string location = Console.ReadLine();
                string band = Console.ReadLine();
                emp1 obj1 = new emp1(id, name, location, band);
                listt.Add(obj1);
            }
            con.Close();
            return listt;
        }
         public int addemp(emp1 obj1)
    {
string connectionstring=@"Data Source=inchnilpdb02\mssqlserver1;Initial Catalog=CHN12_MMS73_TEST;User ID=mms73user;Password=mms73user"; 
             SqlConnection con = new SqlConnection(connectionstring);
             con.Open();
             SqlCommand cmd = new SqlCommand();
             cmd.CommandType = CommandType.StoredProcedure;
             cmd.CommandText = "sp_insertt"; 
             cmd.Connection = con; 
             cmd.Parameters.AddWithValue("@id", obj1.ID);
             cmd.Parameters.AddWithValue("@name", obj1.Name);
             cmd.Parameters.AddWithValue("@location", obj1.Location);
             cmd.Parameters.AddWithValue("@band", obj1.Band); 
             int rowsaff = cmd.ExecuteNonQuery();
             con.Close(); 
             if (rowsaff > 0) 
             { return Convert.ToInt32(cmd.Parameters["@id"].Value); }
             else 
                 return rowsaff; 
          }
    }
}







using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace minefirst
{
    class Program
    {
        static void Main(string[] args)
        {
            empdb obj = new empdb();
        int choice;
        do
        {
            Console.WriteLine("enter your choice");
            choice = Convert.ToInt32(Console.ReadLine());
            switch (choice)
            {
                case 1:

                    Console.WriteLine("enter name");
                    int id = Convert.ToInt32(Console.ReadLine());
                    string name = Console.ReadLine();
                    string location = Console.ReadLine();
                    string band = Console.ReadLine();
                    emp1 e = new emp1(id, name, location, band);
                    int result = obj.addemp(e);
                    Console.WriteLine("customer added " + result);
                    break;
                case 2:
                    Console.WriteLine("enter id");
                    int id1 = Convert.ToInt32(Console.ReadLine());
                    List<emp1> listt = obj.viewemp();

                    foreach(emp1 e1 in listt)
                    {
                        Console.WriteLine(e1.ID);
                        Console.WriteLine(e1.Name);
                        Console.WriteLine(e1.Location);
                        Console.WriteLine(e1.Band);
                    }
                    break;





            }




        } while (choice != 5);
        Console.ReadLine();

     }


        }
    }

