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

namespace Car_Race
{
    public partial class Form1 : Form
    {
        int carspeed = 5;/// the player
        int roadspeed = 5;
        bool carleft, carright;
        int trafficSpeed = 5;
        int score = 0;
        Random ran = new Random();

       
        public Form1()
        {
            InitializeComponent();
            Reset();
        }

        private void label1_Click(object sender, EventArgs e)
        {

        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            score++;
            label2.Text = " " + score;
            road1.Top = road1.Top + roadspeed;
            road2.Top = road2.Top + roadspeed;

            if(road1.Top>630)
            {
                road1.Top = -630;
            }
            if(road2.Top>630)
            {
                road2.Top = -630;
            }
            if(carleft)
            {
                player.Left = player.Left - carspeed;
            }
            if(carright)
            {
                player.Left = player.Left + carspeed;
            }
            if(player.Left<1)
            {
                carleft = false;
            }
            else if(player.Left+player.Width>380)
            {
                carright = false;
            }
        }

        private void Reset()
        {
            button1.Enabled = false;
            trofeu.Visible = false;
            /// boom.visible=false;
            score = 0;
            roadspeed = 5;
            trafficSpeed = 5;

            player.Left = 161;
            player.Top = 286;

            carleft = false;
            carright = false;
            car1.Left = 66;
            car1.Top = -120;

            car2.Left = 294;
            car2.Top = -185;

            road1.Left = -2;
            road1.Top = -638;
            road2.Left = -3;
            road2.Top = -222;

            timer1.Start();
        }
    }
}
