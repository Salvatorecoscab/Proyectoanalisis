# Proyectoanalisis
#include <iostream>
#include <graphics.h>
#include <conio.h>
#include <stdio.h>
#include <math.h>
	using namespace std; 
	int vec[4][2];
	void dibujaplano(int, int, int);

main(){

	//Guardar los datos de los vectores
	cout<<"Este es un programa que te grafica un vector resultante dada la suma de 4 vectores A, B, C, D sobre los ejes coordenados en 2D"<<endl<<endl;
	cout<<"Nota: Las componentes de los vectores solo son numeros enteros."<<endl<<endl;
	
		cout<<"Escriba el largo del vector A: ";
		cin>>vec[0][1];
		vec[0][0]=0;
		cout<<"Escriba el largo del vector B: ";
		cin>>vec[1][0];
		vec[1][0]=-vec[1][0];
		vec[1][1]=0;
		cout<<"Escriba el largo del vector C: ";
		cin>>vec[2][1];
		vec[2][1]=-vec[2][1];
		vec[2][0]=0;
		cout<<"Escriba el largo del vector D: ";
		cin>>vec[3][0];
		vec[3][1]=0;

	cout<<endl<<endl<<"Los vectores ingresados son"<<endl;
	//Muestra vectores
    for (int y = 0; y < 4; y++) {
    	cout<<char(65+y)<<"(";
        for (int x = 0; x < 2; x++) {
            cout<<" "<<vec[y][x]<<" ";
        }
        cout<<")";
        cout<<endl;
    }
	
    int resaAmasbB[2],resCmasresAmasB[2],resTotal[2];
    int a=0,b=0,c=0,d=0;
    int ancho=0,alto=0,lam=0,vent=800,xcero=0,ycero=0;
    	char unidadtexto1[10]="";
    	cout<<endl;
    	cout<<"Inserta el valor de a: ";
		cin>>a;
		cout<<"Inserta el valor de b: ";
		cin>>b;
		cout<<"Inserta el valor de c: ";
		cin>>c;
		cout<<"Inserta el valor de d: ";
		cin>>d;
		
    	resaAmasbB[0]=a*vec[0][0]+b*vec[1][0];
		resaAmasbB[1]=a*vec[0][1]+b*vec[1][1];
		
		resCmasresAmasB[0]=resaAmasbB[0]+c*vec[2][0];
		resCmasresAmasB[1]=resaAmasbB[1]+c*vec[2][1];
		
		resTotal[0]=resCmasresAmasB[0]+d*vec[3][0];
		resTotal[1]=resCmasresAmasB[1]+d*vec[3][1];
		cout<<"La suma de Aa+Bb+Cc+Dd es el vector: ("<<resTotal[0]<<", "<<resTotal[1]<<")"<<endl;
		
		
			    //Encuentra val max para ajustar graf
	    int mayor=vec[0][0];
	    int mayor1=resaAmasbB[0];
	    int mayor2=resCmasresAmasB[0];
	    int mayor3=resTotal[0];
	    
	    for (int y = 0; y < 4; y++) {
	        for (int x = 0; x < 2; x++) {
	            int Actual = abs(vec[y][x]);
	            if (Actual > mayor) mayor = Actual;
	        }
	    }
	        for (int x = 0; x < 2; x++) {
	            int Actual = abs(resaAmasbB[x]);
	            if (Actual > mayor1) mayor1 = Actual;
	        }
	        for (int x = 0; x < 2; x++) {
	            int Actual = abs(resCmasresAmasB[x]);
	            if (Actual > mayor2) mayor2 = Actual;
	        }
	        for (int x = 0; x < 2; x++) {
	            int Actual = abs(resTotal[x]);
	            if (Actual > mayor3) mayor3 = Actual;
	        }
	        
	        int Mmayor[4]={mayor,mayor1,mayor2,mayor3};        
	        int mayor4=Mmayor[0];
	        for (int x = 0; x < 4; x++) {
	            int Actual = abs(Mmayor[x]);
	            if (Actual > mayor4) mayor4 = Actual;
	        }
	    //Multiplicador de unidades..............................
    	lam=vent/(2*mayor4);
    	ancho=2*lam*(mayor4);
    	alto=ancho;
    	xcero=ancho/2;
    	ycero=alto/2;
    	
    	
    	
    	dibujaplano(ancho,alto,lam);
    	

		//A
		setcolor(RED);
		int AV=ycero-lam*vec[0][1];
		if(ycero!=AV)
		line(xcero,ycero,xcero,AV);
		sprintf(unidadtexto1,"A=(%d %d)",vec[0][0],vec[0][1]);
		outtextxy(10,10,unidadtexto1);
		
		//B
		setcolor(GREEN);
		int BV=xcero+lam*vec[1][0];
		if(xcero!=BV)
		line(xcero,ycero,BV,ycero);
		sprintf(unidadtexto1,"B=(%d %d)",vec[1][0],vec[1][1]);
		outtextxy(10,20,unidadtexto1);
		
		//C
		setcolor(BLUE);
		int CV=ycero-lam*vec[2][1];
		if(ycero!=CV)
		line(xcero,ycero,xcero,CV);
		sprintf(unidadtexto1,"C=(%d %d)",vec[2][0],vec[2][1]);
		outtextxy(10,30,unidadtexto1);
		
		//D
		setcolor(CYAN);
		int DV=xcero+lam*vec[3][0];
		if(xcero!=DV)
		line(xcero,ycero,DV,ycero);
		sprintf(unidadtexto1,"D=(%d %d)",vec[3][0],vec[3][1]);
		outtextxy(10,40,unidadtexto1);
		
		//Resultado
		setcolor(YELLOW);
		int xdos=xcero+lam*resTotal[0], ydos=ycero-lam*resTotal[1];
		if((xcero!=xdos)&&(ycero!=ydos))
		line(xcero,ycero,xdos,ydos);
		sprintf(unidadtexto1,"R=(%d %d)",resTotal[0],resTotal[1]);
		outtextxy(10,50,unidadtexto1);
		system("PAUSE>=NULL");
		closegraph();
    		}
    
    
    
void dibujaplano(int an, int al, int la){
	char unidadtexto[10]="";
	//Dibujar el plano bonito bb.........................(HACER FUNCION)
	initwindow(an+100,al+100, "Vectores",0,0);
	
	//Linea horizontal
	setcolor(WHITE);
	line(0,al/2,an,al/2);
	//Linea vertical
	setcolor(WHITE);
	line(an/2,0,an/2,al);
	setcolor(WHITE);
	
	int ciclo1=0,ciclo2=0;
		//Lineas verticales
	for(int i=0;i<=an;i=i+la){
		line(i,al/2-4,i,al/2+4);
		ciclo1++;
	}
	for(int i=0;i<=an;i=i+la){
		sprintf(unidadtexto,"%d",i/la-ciclo1/2);
		outtextxy(i+4,al/2+20,unidadtexto);
	}
	//Lineas horizontales
	for(int i=0;i<=al;i=i+la){
		line(an/2-4,i,an/2+4,i);
		ciclo2++;
	}
	for(int i=0;i<=al;i=i+la){
		sprintf(unidadtexto,"%d",-(i/la-ciclo2/2));
		outtextxy(an/2+20,i+4,unidadtexto);
	}
	}
