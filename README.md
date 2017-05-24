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
        string[] split;
        string[] split1;
        int N, U, D, I, J, L, K;
        int len;
        //int [] Fl=new int[100000];
        List <int> list= new List<int>();
        int[,] AM;
        int Nindex;

        string ReverseString(string s)
        {
            char[] arr = s.ToCharArray();
            Array.Reverse(arr);
            return new string(arr);
        }

        void VstavMassiv(int n)
        {
           if(!list.Contains(n))
               list.Add(n);
        }

        void ListOut()
        {
            int[] myArray = list.ToArray();
            string ttt = "";
            for (int i = 0; i < myArray.Length; i++)
            {
                ttt = ttt + myArray[i].ToString() + ", ";
            }
            listBox1.Items.Add(ttt);
        }

        void EasyZ(int []myArray)
        {
            len = myArray.Length;
            dataGridView1.RowCount = len;
            dataGridView1.AutoSizeColumnsMode = DataGridViewAutoSizeColumnsMode.Fill;
            dataGridView1.ColumnCount = len;
            AM = new int[len, len];
            for(int i=0; i<len; i++)
            {
                
                for (int j = 0; j <= i; j++)
                {
                    if (i == j)
                        AM[i, j] = 0;
                    AM[i, j] = (myArray[i] - myArray[j]) * D;
                }
                for(int j=i+1; j<len; j++)
                {
                    AM[i, j] = (myArray[j] - myArray[i]) * U;
                }
            }
            //for (int i = 0; i < len; i++)
              //for (int j = 0; j < len; j++)
                //   dataGridView1.Rows[i].Cells[j].Value = AM[i, j];

        }

        int Indexx(int n, int[] myArray)
        {
            int ind=1;
            for(int i=0; i<myArray.Length; i++)
            {
                if (myArray[i] == n)
                    ind = i;
            }
            return ind;
        }

        void Mindist(string[] split, int K, int [,] AM, int[] myArray)
        {
            for(int i=1; i<=K; i++)
            {
                for(int j=1; j<=K; j++)
                {
                    if(i!=j)
                    {
                        if (AM[Indexx(Convert.ToInt32(split[i]), myArray), Indexx(Convert.ToInt32(split[j]), myArray)] > (I + J))
                            AM[Indexx(Convert.ToInt32(split[i]), myArray), Indexx(Convert.ToInt32(split[j]), myArray)] = (I + J);
                    }

                }
            }
        }
        int[] Dek;
        int[] minvers;
        void Deikstra()
        {
           Dek = new int[len];
            minvers = new int[len];
            bool[] used = new bool[len];
            for (int i = 0; i < len; i++)
            {

                Dek[i] = 1000001;
                used[i] = false;
            }
            Dek[0] = 0;
            minvers[0] = 0;
            int minindex;
            int min;
            int tempv = 0;
            do
            {
                minindex = 1000001;
                min = 1000001;
                for (int i = 0; i < len; i++)
                {
                    if (!used[i] && Dek[i] < min)
                    {
                        min = Dek[i];
                        minindex = i;
                        //listBox2.Items.Add(minindex + 1);
                    }
                }
                if (minindex != 1000001)
                {
                    for (int i = 0; i < len; i++)
                    {
                        if (AM[minindex, i] > 0)
                        {
                            tempv = min + AM[minindex, i];
                            if (tempv < Dek[i])
                            {
                                Dek[i] = tempv;
                                minvers[i] = minindex + 1;
                            }
                        }
                    }
                    used[minindex] = true;
                }
            } while (minindex < 1000001);

        }


         void Marshrut(int[] myArray)
            {
               int xx=-1;
               int el=0;
               int last = Nindex+1;
               string ttt = Convert.ToString(N);
                while(xx!=1)
                {
                    xx=minvers[last-1];
                    //ttt = ttt + "-" + Convert.ToString(myArray[xx-1]);
                    ttt = Convert.ToString(myArray[xx - 1])+"--"+ttt;
                    last = xx;
                    last = xx;
                }
                    // ttt=ReverseString(ttt);
                    listBox1.Items.Add(ttt);
            }

        private void button1_Click(object sender, EventArgs e)
        {

            listBox1.Items.Clear();
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
            EasyZ(myArray);
            ListOut();
            for (int i = 1; i <= L; i++)
            {
                temp = s[i];
                split1 = temp.Split(new char[] { ' ' }, StringSplitOptions.RemoveEmptyEntries);
                K = Convert.ToInt32(split1[0]);
                Mindist(split1, K, AM, myArray);

            }
            for (int i = 0; i < len; i++)
                for (int j = 0; j < len; j++)
                    dataGridView1.Rows[i].Cells[j].Value = AM[i, j];
            Deikstra();
            Nindex = Indexx(N, myArray);
            if (Dek[Nindex] == 1000001)
                Dek[Nindex] = 0;
                listBox1.Items.Add("Щоб підняти сейф на " + N + " поверх Віті потрібно: " + Dek[Nindex]);
                Marshrut(myArray);
        }
    }
}
