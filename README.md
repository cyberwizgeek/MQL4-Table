# MQL4-Table
A library for creating mql4 table

Usage:

1. Put the file in the MQL4\Inclue folder

2. In your indicator/expert/script type #include <Table.mqh>

3. Declare your table by: Table *myTable = new Table(ChartID(), Subwindows, "tableName");

4. Initialize your table by calling: 
    myTable.Create();  //use the default values; or
    myTable.Create(int x=0, int y=0, int w=0, int h=0, int xOffset=3, int yOffset=3, int cellWidth=0, int cellHeight=0, int cellSpace=2, int fontSize=8, string fontName="Terminal") //to set each value as you wishes

5. Create a 2-Dimensional string array to story your data: string cells[rows][cols] //as MQL4 don't not support 2-D dynamic array, therefore, currently only support static 2-D array.

6. To show your table: myTable.Show(cells);

Features:

1.  Auto cell-size

2.  Auto table-size (as default window size)

3.  Alternativate Color scheme: (under-testing)

Public method description
		
		void	Table(long id, int subwin, string name);  	//default constructor  
		//id:     the id of the chart, ChartID(), which the table will show
		//subwin: the indicator window which the table will show, should >=0
		//name:   unique name of the table, you can show more than one table in the chart by using different names
		
		//default initializer
		void 		Create( int x=0, int y=0,   //table top-left coner co-ordinates with default values of (0,0)
		                int w=0, int h=0,           //table width & height; default value 0 means use whole subwin size
		                int xOffset=3, int yOffset=3,       //the cell's x-y offset related to the table top-left coner
		                int cellWidth=0, int cellHeight=0,  //width & height of the cells default value 0 means auto size
		                int cellSpace=2,                    //cellspace between each cell;
		                int fontSize=8,                     //fontsize of the text
		                string fontName="Terminal");        //font used in the table
		                
		void 		SetFontColors(color fontColor, color altFontColor);
		
		void 		SetBgColors(color bgColor, color cellBgColor);
		
		void 		SetAltFontColorMode(ENUM_ALT_COLOR_MODE altMode){//not yet implement}
		
		bool 		Show(string &cells[][]);                    //Render the table
		
		void		~Table();                                   //Delete table and remove all objects created by the table.




# Sample Code
```
#property copyright "Copyright 2021, MetaQuotes Software Corp."
#property link      "https://www.mql5.com"
#property version   "1.00"

#include <Table.mqh>


//+------------------------------------------------------------------+
//| Expert initialization function                                   |
//+------------------------------------------------------------------+
int OnInit()
  {
//---

   string myArray[10][10];
   

   
   Table *myTable = new Table(ChartID(), 0, "tableName");
   myTable.Create(0,0,10,10); //to set each value as you wishes

   myArray[0][0] ="ID";
   myArray[0][1] ="Name";
   myArray[1][0] ="1";
   myArray[1][1] ="test";
   myArray[2][0] ="2";
   myArray[2][1] ="test2";
  
   myTable.Show(myArray);
   


//---
   return(INIT_SUCCEEDED);
  }
//+------------------------------------------------------------------+
//| Expert deinitialization function                                 |
//+------------------------------------------------------------------+
void OnDeinit(const int reason)
  {
//---
   
  }
//+------------------------------------------------------------------+
//| Expert tick function                                             |
//+------------------------------------------------------------------+
void OnTick()
  {
//---
   
  }
//+------------------------------------------------------------------+


```
