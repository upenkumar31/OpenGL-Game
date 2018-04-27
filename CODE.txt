#include <GL/glut.h> 
#include <stdio.h>   
#include <stdlib.h>        
#include <string.h>
void reshape (int ,int);
void O(int , int , int , int );
void X(int , int , int , int );
void mouse(int, int , int , int );
void view(void);
void text( int ,int , char *);
void strat(int);
void draw(void);
void loose(void);
void win(void);
void result(void);
int mx, my, Wx, Wy, mo;
int dbox[9];
int mb[9][2] = {{-6,6},{0,6},{6,6},{-6,0},{0,0},{6,0},{-6,-6},{0,-6},{6,-6}};
void cir(int);
static int a[9]={0,0,0,0,0,0,0,0,0};
static int b[9]={0,0,0,0,0,0,0,0,0};
GLUquadricObj *Cylinder;
void text( int x, int y, char *ch)
{
	int l,i;

	l=strlen( ch ); 
	glRasterPos2f( x, y);
	for( i=0; i < l; i++) 
		{
			glutBitmapCharacter(GLUT_BITMAP_TIMES_ROMAN_24, ch[i]);
	}

}


void init(void)
{
   glClearColor (0.0, 0.0, 0.0, 0.0);
   Cylinder = gluNewQuadric();
   gluQuadricDrawStyle( Cylinder, GLU_FILL );
   gluQuadricNormals( Cylinder, GLU_SMOOTH );
}


void O(int x, int y, int z, int a)
{
glColor3f(1, 0,0);
glPushMatrix();
glTranslatef(x, y, z);
glPushMatrix();
glutSolidTorus(0.5, 2.0, 8, 16);
glPopMatrix();

}


void X(int x, int y, int z, int a)
{
glColor3f(0.0, 0.0, 1.0);
glPushMatrix();
glTranslatef(x, y, z);
glPushMatrix();
glRotatef(a, 1, 0, 0);
glRotatef(90, 0, 1, 0);
glRotatef(45, 1, 0, 0);
glTranslatef( 0, 0, -3);
gluCylinder( Cylinder, 0.5, 0.5, 6, 16, 16);
glPopMatrix();
glPushMatrix();
glRotatef(a, 1, 0, 0);
glRotatef(90, 0, 1, 0);
glRotatef(315, 1, 0, 0);
glTranslatef( 0, 0, -3);
gluCylinder( Cylinder, 0.5, 0.5, 6, 16, 16);
glPopMatrix();
}

void mouse(int button, int state, int x, int y)
{
mx =  (18 * (float) ((float)x/(float)Wx))/6;
my =  (18 * (float) ((float)y/(float)Wy))/6;
mo= mx + my * 3;
if ((button==GLUT_LEFT_BUTTON)&&(state==GLUT_DOWN))
{
	
	glMatrixMode (GL_PROJECTION); 
	glLoadIdentity();  
	glOrtho(-9.0, 9.0, -9.0, 9.0, 0.0, 30.0);
	glMatrixMode(GL_MODELVIEW);  
	glLoadIdentity();
	X(mb[mo][0],mb[mo][1], -1, 1);
	a[mo]=1;	
	dbox[mo]=1;	
	strat(mo);
}

glutSwapBuffers();
}

void result()
{

if((a[0]==1&&a[1]==1&&a[2]==1)||(a[0]==1&&a[3]==1&&a[6]==1)||(a[2]==1&&a[5]==1&&a[8]==1)||(a[6]==1&&a[7]==1&&a[8]==1)||(a[0]==1&&a[4]==1&&a[8]==1)||(a[2]==1&&a[4]==1&&a[6]==1)||(a[3]==1&&a[4]==1&&a[5]==1)||(a[3]==1&&a[4]==1&&a[5]==1))
{win();}
				

else if((b[0]==1&&b[1]==1&&b[2]==1)||(b[0]==1&&b[3]==1&&b[6]==1)||(b[2]==1&&b[5]==1&&b[8]==1)||(b[6]==1&&b[7]==1&&b[8]==1)||(b[0]==1&&b[4]==1&&b[8]==1)||(b[2]==1&&b[4]==1&&b[6]==1)||(b[3]==1&&b[4]==1&&b[5]==1)||(b[1]==1&&b[4]==1&&b[7]==1))
{loose();}

else if(dbox[0]==1&&dbox[1]==1&&dbox[2]==1&&dbox[3]==1&&dbox[4]==1&&dbox[5]==1&&dbox[6]==1&&dbox[7]==1&&dbox[8]==1)
draw();
}

void strat(int t)
{
int i;

	while(1){       if(b[0]==0&&b[1]==1&&b[2]==1&&a[0]==0){b[0]=1;dbox[0]=1;cir(0);break;}
			if(b[0]==1&&b[1]==0&&b[2]==1&&a[1]==0){b[1]=1;dbox[1]=1;cir(1);break;}
			if(b[0]==1&&b[1]==1&&b[2]==0&&a[2]==0){b[2]=1;dbox[2]=1;cir(2);break;}
			
			
			if(b[3]==0&&b[4]==1&&b[5]==1&&a[3]==0){b[3]=1;dbox[3]=1;cir(3);break;}
			if(b[3]==1&&b[4]==0&&b[5]==1&&a[4]==0){b[4]=1;dbox[4]=1;cir(4);break;}
			if(b[3]==1&&b[4]==1&&b[5]==0&&a[5]==0){b[5]=1;dbox[5]=1;cir(5);break;}

			if(b[6]==0&&b[7]==1&&b[8]==1&&a[6]==0){b[6]=1;dbox[6]=1;cir(6);break;}
			if(b[6]==1&&b[7]==0&&b[8]==1&&a[7]==0){b[7]=1;dbox[7]=1;cir(7);break;}
			if(b[6]==1&&b[7]==1&&b[8]==0&&a[8]==0){b[8]=1;dbox[8]=1;cir(8);break;}

			if(b[0]==0&&b[3]==1&&b[6]==1&&a[0]==0){b[0]=1;dbox[0]=1;cir(0);break;}
			if(b[0]==1&&b[3]==0&&b[6]==1&&a[3]==0){b[3]=1;dbox[3]=1;cir(3);break;}
			if(b[0]==1&&b[3]==1&&b[6]==0&&a[6]==0){b[6]=1;dbox[6]=1;cir(6);break;}

			if(b[2]==0&&b[5]==1&&b[8]==1&&a[2]==0){b[2]=1;dbox[2]=1;cir(2);break;}
			if(b[2]==1&&b[5]==0&&b[8]==1&&a[5]==0){b[5]=1;dbox[5]=1;cir(5);break;}
			if(b[2]==1&&b[5]==1&&b[8]==0&&a[8]==0){b[8]=1;dbox[8]=1;cir(8);break;}

			if(b[0]==0&&b[4]==1&&b[8]==1&&a[0]==0){b[0]=1;dbox[0]=1;cir(0);break;}
			if(b[0]==1&&b[4]==0&&b[8]==1&&a[4]==0){b[4]=1;dbox[4]=1;cir(4);break;}
			if(b[0]==1&&b[4]==1&&b[8]==0&&a[8]==0){b[8]=1;dbox[8]=1;cir(8);break;}

			if(b[2]==0&&b[4]==1&&b[6]==1&&a[2]==0){b[2]=1;dbox[2]=1;cir(2);break;}
			if(b[2]==1&&b[4]==0&&b[6]==1&&a[4]==0){b[4]=1;dbox[4]=1;cir(4);break;}
			if(b[2]==1&&b[4]==1&&b[6]==0&&a[6]==0){b[6]=1;dbox[6]=1;cir(6);break;}

			if(b[1]==0&&b[4]==1&&b[7]==1&&a[1]==0){b[1]=1;dbox[1]=1;cir(1);break;}
			if(b[1]==1&&b[4]==0&&b[7]==1&&a[4]==0){b[4]=1;dbox[4]=1;cir(4);break;}
			if(b[1]==1&&b[4]==1&&b[7]==0&&a[7]==0){b[7]=1;dbox[7]=1;cir(7);break;}
			
			

			if(a[2]==0&&a[0]==1&&a[1]==1&&b[2]==0){b[2]=1;dbox[2]=1;cir(2);break;}
			if(a[1]==0&&a[0]==1&&b[1]==0&&a[2]==1){b[1]=1;dbox[1]=1;cir(1);break;}
			if(a[0]==0&&b[0]==0&&a[1]==1&&a[2]==1){b[0]=1;dbox[0]=1;cir(0);break;}
			
			if(a[6]==0&&a[0]==1&&a[3]==1&&b[6]==0){b[6]=1;dbox[6]=1;cir(6);break;}
			if(a[3]==0&&a[0]==1&&b[3]==0&&a[6]==1){b[3]=1;dbox[3]=1;cir(3);break;}
			if(a[0]==0&&b[0]==0&&a[3]==1&&a[6]==1){b[0]=1;dbox[0]=1;cir(0);break;}
			
			if(a[8]==0&&a[2]==1&&a[5]==1&&b[8]==0){b[8]=1;dbox[8]=1;cir(8);break;}
			if(a[5]==0&&a[2]==1&&b[5]==0&&a[8]==1){b[5]=1;dbox[5]=1;cir(5);break;}
			if(a[2]==0&&b[2]==0&&a[5]==1&&a[8]==1){b[2]=1;dbox[2]=1;cir(2);break;}
			
			if(a[8]==0&&a[6]==1&&a[7]==1&&b[8]==0){b[8]=1;dbox[8]=1;cir(8);break;}
			if(a[7]==0&&a[6]==1&&b[7]==0&&a[8]==1){b[7]=1;dbox[7]=1;cir(7);break;}
			if(a[6]==0&&b[6]==0&&a[7]==1&&a[8]==1){b[6]=1;dbox[6]=1;cir(6);break;}
			
			if(a[5]==0&&a[3]==1&&a[4]==1&&b[5]==0){b[5]=1;dbox[5]=1;cir(5);break;}
			if(a[4]==0&&a[3]==1&&b[4]==0&&a[5]==1){b[4]=1;dbox[4]=1;cir(4);break;}
			if(a[3]==0&&b[3]==0&&a[4]==1&&a[5]==1){b[3]=1;dbox[3]=1;cir(3);break;}

			if(a[6]==0&&a[2]==1&&a[4]==1&&b[6]==0){b[6]=1;dbox[6]=1;cir(6);break;}
			if(a[4]==0&&a[2]==1&&b[4]==0&&a[6]==1){b[4]=1;dbox[4]=1;cir(4);break;}
			if(a[2]==0&&b[2]==0&&a[4]==1&&a[6]==1){b[2]=1;dbox[2]=1;cir(2);break;}

			if(a[8]==0&&a[0]==1&&a[4]==1&&b[8]==0){b[8]=1;dbox[8]=1;cir(8);break;}
			if(a[4]==0&&a[0]==1&&b[4]==0&&a[8]==1){b[4]=1;dbox[4]=1;cir(4);break;}
			if(a[0]==0&&b[0]==0&&a[4]==1&&a[8]==1){b[0]=1;dbox[0]=1;cir(0);break;}

			if(a[7]==0&&a[1]==1&&a[4]==1&&b[7]==0){b[7]=1;dbox[7]=1;cir(7);break;}
			if(a[4]==0&&a[1]==1&&b[4]==0&&a[7]==1){b[4]=1;dbox[4]=1;cir(4);break;}
			if(a[1]==0&&b[1]==0&&a[4]==1&&a[7]==1){b[1]=1;dbox[1]=1;cir(1);break;}


			

			if(a[4]==0&&b[4]==0&&(t==0||t==1||t==2)){b[4]=1;dbox[4]=1;cir(4);break;}
		        if(a[7]==0&&b[7]==0&&(t==0||t==1||t==2)){b[7]=1;dbox[7]=1;cir(7);break;}		
			if(a[8]==0&&b[8]==0&&(t==0||t==1||t==2)){b[8]=1;dbox[8]=1;cir(8);break;}
			if(a[6]==0&&b[6]==0&&(t==0||t==1||t==2)){b[6]=1;dbox[6]=1;cir(6);break;}
			if(a[5]==0&&b[5]==0&&(t==0||t==1||t==2)){b[5]=1;dbox[5]=1;cir(5);break;}
			if(a[3]==0&&b[3]==0&&(t==0||t==1||t==2)){b[3]=1;dbox[3]=1;cir(3);break;}

			if(a[2]==0&&b[2]==0&&(t==3||t==4||t==5)){b[2]=1;dbox[2]=1;cir(2);break;}		
			if(a[7]==0&&b[7]==0&&(t==3||t==4||t==5)){b[7]=1;dbox[7]=1;cir(7);break;}		
			if(a[0]==0&&b[0]==0&&(t==3||t==4||t==5)){b[0]=1;dbox[0]=1;cir(0);break;}
			if(a[6]==0&&b[6]==0&&(t==3||t==4||t==5)){b[6]=1;dbox[6]=1;cir(6);break;}
			if(a[8]==0&&b[8]==0&&(t==3||t==4||t==5)){b[8]=1;dbox[8]=1;cir(8);break;}
			if(a[1]==0&&b[1]==0&&(t==3||t==4||t==5)){b[1]=1;dbox[1]=1;cir(1);break;}

			if(a[4]==0&&b[4]==0&&(t==6||t==7||t==8)){b[4]=1;dbox[4]=1;cir(4);break;}
			if(a[1]==0&&b[1]==0&&(t==6||t==7||t==8)){b[1]=1;dbox[1]=1;cir(1);break;}
			if(a[0]==0&&b[0]==0&&(t==6||t==7||t==8)){b[0]=1;dbox[0]=1;cir(0);break;}
			if(a[5]==0&&b[5]==0&&(t==6||t==7||t==8)){b[5]=1;dbox[5]=1;cir(5);break;}
			if(a[3]==0&&b[3]==0&&(t==6||t==7||t==8)){b[3]=1;dbox[3]=1;cir(3);break;}
			if(a[2]==0&&b[2]==0&&(t==6||t==7||t==8)){b[2]=1;dbox[2]=1;cir(2);break;}
					
			if(t==0||t==1||t==2||t==3||t==4||t==5||t==6||t==7||t==8)
			result();
		}

result();
}
void cir(int i)
{
glMatrixMode (GL_PROJECTION); 
glLoadIdentity();  
glOrtho(-9.0, 9.0, -9.0, 9.0, 0.0, 30.0);
glMatrixMode(GL_MODELVIEW);  
glLoadIdentity();
O(mb[i][0],mb[i][1], -1, 1);
glutSwapBuffers();
}
void view(void)
{
int x, y;
int i;
int j;

glClear (GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

glMatrixMode (GL_PROJECTION); 
glLoadIdentity();  
glOrtho(-9.0, 9.0, -9.0, 9.0, 0.0, 30.0);
glMatrixMode(GL_MODELVIEW);  
glLoadIdentity();


glColor3f(0.0, 0.0, 1.0);
for( x = 0; x < 4; x++)
	{
       		glPushMatrix();
       		glColor3f(1,1,1);
	   	glBegin(GL_LINES);
	   	glVertex2i(-9 , -9 + x * 6);
	   	glVertex2i(9 , -9 + x * 6 );
	   	glEnd();
	   	glPopMatrix();
	}
	for( y = 0; y < 4; y++ )
	   {
       		glPushMatrix();
       		glColor3f(1,1,1);
	   	glBegin(GL_LINES);
	   	glVertex2i(-9 + y * 6, 9 );
	   	glVertex2i(-9 + y * 6, -9 );
	   	glEnd();
	   	glPopMatrix();
	   }
glutSwapBuffers();
}


void draw()
{
glColor3f(1,1,1);
text(0,0,"TIE");
}


void loose()
{
glColor3f(1,1,1);
text(0,0,"YOU LOOSE");
}


void win()
{
glColor3f(1,1,1);
text(0,0,"YOU WIN");
}

void reshape (int w, int h)
{
   Wx = w;
   Wy = h;
   glViewport (0, 0, (GLsizei) w, (GLsizei) h);
   glMatrixMode (GL_PROJECTION);
   glLoadIdentity ();
}


int main(int argc, char* argv[])
{
   glutInit(&argc, argv);
   glutInitDisplayMode (GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH);
   glutInitWindowSize (500, 500);
   glutInitWindowPosition (20, 20);
   glutCreateWindow (argv[0]);
   glutSetWindowTitle("TIC TAC TOE");
   init ();
   glutReshapeFunc(reshape);
   glutMouseFunc(mouse);
   glutDisplayFunc(view);
   glutMainLoop();

   return 0;
}



