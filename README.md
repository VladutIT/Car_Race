//////////////////////////////////////////////////////////THE CODE///////////////////////////////////////////////////////////////////////////////////////////////////////





using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Race_Car
{
    public partial class Form1 : Form
    {
        int carspeed = 5;
        int roadspeed = 5;
        bool carLeft, carRight;
        int trafficspeed = 5;
        int score = 0;
        Random rnd = new Random();
        public Form1()
        {
            InitializeComponent();
            Reset();
        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            score++;
            label1.Text = "Distanta " + score;
            pictureBox1.Top = pictureBox1.Top + roadspeed;
            pictureBox2.Top = pictureBox2.Top + roadspeed;
            if(pictureBox1.Top>650)
            {
                pictureBox1.Top = -660;
            }
            if(pictureBox2.Top>650)
            {
                pictureBox2.Top = -660;
            }
            if(carLeft)
            {
                player.Left = player.Left - carspeed;
            }
            if(carRight)
            {
                player.Left = player.Left + carspeed;
            }
            if(player.Left<1)
            {
                carLeft = false;
            }
            else if(player.Left+player.Width>380)
            {
                carRight = false;
            }
            car1.Top = car1.Top + trafficspeed;
            car2.Top = car2.Top + trafficspeed;
            if(car1.Top>panel1.Height)
            {
                changecar1();
                car1.Left = rnd.Next(2, 160);
                car1.Top = rnd.Next(100, 200) * -1;
            }
            if(car1.Top>panel1.Height)
            {
                changecar2();
                car2.Left = rnd.Next(185, 327);
                car2.Top = rnd.Next(100, 200) * -1;
            }
            if(player.Bounds.IntersectsWith(car1.Bounds) || player.Bounds.IntersectsWith(car2.Bounds))
            {
                Gameover();
            }
            if(score>100 && score<500)
            {
                trafficspeed = 6;
                roadspeed = 7;
            }
            else if(score>500 && score<100)
            {
                trafficspeed = 7;
                   roadspeed = 8;
            }
            else if(score>1200)
            {
                trafficspeed = 9;
                roadspeed = 10;
            }
        }

        private void Reset()
        {
            trofeu.Visible = false;
            button1.Enabled = false;
            explosion.Visible = false;
            trafficspeed = 5;
            roadspeed = 5;
            score = 0;
            player.Left = 161;
            player.Top = 286;
            carLeft = false;
            carRight = false;
            car1.Left = 66;
            car1.Top = -120;
            car2.Left = 294;
            car2.Top = -185;
            timer1.Start();
        }
        private void masina_directie(object sender,KeyEventArgs e)
        {
            if(e.KeyCode==Keys.Left && player.Left>=1)
            {
                carLeft = true;
            }
            if(e.KeyCode == Keys.Right && player.Left + player.Width < panel1.Width)
            {
                carRight = true;
            }
        }

        private void button1_Click(object sender, EventArgs e)
        {
            Reset();
        }

        private void stop(object sender,KeyEventArgs e)
        {
            if(e.KeyCode==Keys.Left)
            {
                carLeft = false;
            }
            if (e.KeyCode == Keys.Right)
            {
                carRight = false;
            }
        }
        private void Gameover()
        {
            trofeu.Visible = true;
            timer1.Stop();
            explosion.Visible = true;
            player.Controls.Add(explosion);
            explosion.Location = new Point(11, 3);
            explosion.BackColor = Color.Transparent;
            explosion.BringToFront();
            button1.Enabled = true;
            if(score<2000)
            {
                trofeu.Image = Properties.Resources.Locul3;
            }
            else if(score>=2000 && score<=3500)
            {
                trofeu.Image = Properties.Resources.Locul2;
            }
            else if(score>3500)
            {
                trofeu.Image = Properties.Resources.Primuloc;
            }
           
        }
       private void changecar1()
        {
            int num = rnd.Next(1, 5);

            switch(num)
            {
                case 1:
            car1.Image = Properties.Resources.Car1;
            break;
                case 2:
                    car1.Image = Properties.Resources.Car2;
            break;
                case 3:
            car1.Image = Properties.Resources.Car3;
            break;
                case 4:
            car1.Image = Properties.Resources.Car4;
            break;
                case 5:
                    car1.Image = Properties.Resources.Car4;
                    break;
                default:
                break;
            }
        }

        private void pictureBox2_Click(object sender, EventArgs e)
        {

        }

        private void changecar2()
        {
            int nr = rnd.Next(1, 5);
            switch (nr)
            {
                case 1:
                    car2.Image = Properties.Resources.Car1;
                    break;
                case 2:
                    car2.Image = Properties.Resources.Car2;
                    break;
                case 3:
                    car2.Image = Properties.Resources.Car3;
                    break;
                case 4:
                    car2.Image = Properties.Resources.Car4;
                    break;
                case 5:
                    car2.Image = Properties.Resources.Car4;
                    break;
                default:
                    break;
            }

        }
    }
}

