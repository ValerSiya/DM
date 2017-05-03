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
        int N, U, D, I, J, L;
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
            for(int i=1; i<L; i++)
            {

            }

        }
    }
}
