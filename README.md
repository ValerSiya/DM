# DM
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.IO;
using System.Collections;


namespace Elevator
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        string[] s;
        string temp;
        string elev;
        string[] split;
        string[] split1;
        int N, U, D, I, J, L, K;
        int len=2;
        //int [] Fl=new int[100000];
        List <int> list= new List<int>();
        void VstavMassiv(int n)
        {
           if(!list.Contains(n))
           {
               list.Add(n);
           }
        }

        void ListOut()
        {
            
        
            int[] myArray = list.ToArray();
            string ttt = "";
            for (int i = 0; i < myArray.Length; i++)
            {
                ttt = ttt + myArray[i].ToString()+", ";
            }
            listBox1.Items.Add(ttt);
        
        }
        private void button1_Click(object sender, EventArgs e)
        {
            s = File.ReadAllLines("info.txt");
            temp = s[0];
            split = temp.Split(new char[] { ' ' }, StringSplitOptions.RemoveEmptyEntries);
            N = Convert.ToInt32(split[0]);
            U= Convert.ToInt32(split[1]);
            D = Convert.ToInt32(split[2]);
            I = Convert.ToInt32(split[3]);
            J = Convert.ToInt32(split[4]);
            L = Convert.ToInt32(split[5]);
            list.Add(1);
            list.Add(N);
            for(int i=1; i<=L; i++)
            {
                temp = s[i];
                split1=temp.Split(new char[] { ' ' }, StringSplitOptions.RemoveEmptyEntries);
                K = Convert.ToInt32(split1[0]);
                for(int k=1; k<=K; k++)
                {
                    VstavMassiv(Convert.ToInt32(split1[k]));
                }
            }
            list.Sort();
            int[] myArray = list.ToArray();
            ListOut();


        }
    }
}
