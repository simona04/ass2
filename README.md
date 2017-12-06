# ass2
//-----------------------------------------------------------------------------
// ass2.c
//
// 
//
// Group: A study assistant Paul Nagele  
//
// Authors: 
//
// Latest Changes: 
//-----------------------------------------------------------------------------
//
//Includes
#include <stdio.h>    
#include <stdlib.h>   
#include <string.h>
#include <inttypes.h>
#include <math.h>

typedef struct tagBITMAPINFOHEADER 
{
    uint32_t   biSize;
    int32_t   biWidth;
    int32_t   biHeight;
    uint16_t   biPlanes;
    uint16_t   biBitCount;
    uint32_t   biCompression;
    uint32_t   biSizeImage;
    int32_t   biXPelsPerMeter;
    int32_t   biYPelsPerMeter;
    uint32_t   biClrUsed;
    uint32_t   biClrImportant;
} __attribute__((packed)) BITMAPINFOHEADER;

typedef struct tagBITMAPFILEHEADER
{
    uint16_t    bfType;
    uint32_t   bfSize;
    uint32_t   bfReserved;
    uint32_t   bfOffBits;
} __attribute__((packed)) BITMAPFILEHEADER;

typedef struct color_
{ 
  uint8_t B;
  uint8_t G;
  uint8_t R; 
}pixel;

//Struct declaration for our input parameters
typedef struct construct_
{
  
  int type;         //Rectangle, Triangle, Circle?
  int id;           //id (int)
  int color;        //what color
  int parameter_1;  //parameter 1-6, position parameter
  int parameter_2;
  int parameter_3;
  int parameter_4;
  int parameter_5;  
  int parameter_6;  
  struct construct *next_construct; //chained list, pointer to next element
  
}construct_;  

int picklines(char *filename); /*read line, pointer to txtfile,
"2D Array" for lines string=array of chars, line=array of strings*/
//int analysisLines(char **lines, int parametervect[], int column);
//int appendListElement(int parametervect[], int dye_numb, construct *first_construct);
//void printoutList(construct *first_construct);
//void bootPixels(pixel **pixels, int width, int height);
//void initBmp(BITMAPFILEHEADER *bmfileh, BITMAPINFOHEADER *bminfoh, int width, int height);
//int writeBmp(BITMAPFILEHEADER *bmfileh, BITMAPINFOHEADER *bminfoh, char *output, pixel **pixels, int width, int height);
//void drawCirc(char *color, int CenterX, int CenterY, int Radius, pixel **pixels, int width, int height);
//void drawTri(char *color, int aX, int aY, int bX, int bY, int cX, int cY, pixel **pixels, int width, int height);
//void drawRect(char *color, int beginnX, int beginnY, int endX, int endY, pixel **pixels, int width, int height);

int main(int argc, char *argv[])   //argc=Argument Count, argv=Argument Values
{
  char *filename = argv[1];      //Inputfile <>.txt
  //char *bmpname = argv[2];     //Outputfile <>.bmp
  //int width = atoi(argv[3]);  //with of bitmap
  //int height = atoi(argv[4]); //height of Bitmap
  
  //int parametervect[9];    //construct struct parameter in Array
  
  int column; 
  column = picklines (filename, first_construct); //Function call, return column
  
  construct_ *first_construct = NULL;
  /*
  
  for(int linecount = 0; linecount < column; linecount++)
  {
    int dye_numb = analysisLines(lines, parametervect, linecount); 
    //Color Number, return numb from function
    appendListElement(parametervect, dye_numb, first_construct);
    //append new Element, return 0, !!!Wieso keine void Funktion?!!!
  }
  
  printoutList(first_construct);  //Liste ausgeben
  
  //...Bytes hinzufügen
  if(width % 4 == 1)
  {
    width = width +3;
  }
  if(width % 4 == 2)
  {
    width = width +2;
  }
  if(width % 4 == 3)
  {
    width = width+1;
  }
  //The with must be divided by 4 for the bitmap
  
  pixel **pixels = malloc(height * 3 * 8);  
  //Memory for height and Color (3(RGB)*8(Bytes))
  if(pixels != NULL)
  {
    for (int pixelcount = 0; pixelcount < height; pixelcount++)
    {
      pixels[pixelcount] = malloc(width * 3 * 8);
      if(pixels[pixelcount] == NULL)
      {
        return 0;
      }
    }
  }
  else
    return 0;
  
  bootPixels(pixels, width, height);
  drawRect(color, beginnX, beginnY, endX, endY, pixels, width, height);
  
  
  BITMAPFILEHEADER bmfileh;
  BITMAPINFOHEADER bminfoh;
  
  initBmp(&bmfileh, &bminfoh, width, height);
  writeBmp(&bmfileh, &bminfoh, output, pixels, width, height);
  
  free(lines);
  */
  return 0;
}

//-----------------------------------------------------------------------------
//int picklines(FILE *txt, char **lines)
//
//-----------------------------------------------------------------------------
int picklines(char *filename, construct_ *first_construct)
{
  form *new_construct
  char c;
  
  int id;
  char color[6];
  int parameter_1;
  int parameter_2;
  int parameter_3;
  int parameter_4;
  int parameter_5;
  int parameter_6;
  
  FILE *inputFile;
  
  inputFile = fopen(filename,"r"); //Open the txt file
  if (inputFile == NULL)  //If there insn't any file, "ERROR"
  {
    return 0;
  }
    
  // File open
  c = getc(inputFile);
  
  switch(c)
  {
    case 'r':
    fscanf(inputFile,"ectangle id=\"%d\" color=\"%c%c%c%c%c%c\" x=\"%d\" y=\"%d\" width=\"&d\" height=\"%d\"", &id,&color[0],&color[1],&color[2],&color[3],&color[4],&color[5],&parameter_1,&parameter_2,&parameter_3,&parameter_4);
    new_construct(id,color,parameter_1,parameter_2,parameter_3,parameter_4);
    break;
    
    case 'c':
    fscanf(inputFile,"ircle id=\"%d\" color=\"%c%c%c%c%c%c\" x=\"%d\" y=\"%d\" radius=\"%d\"", &id,&color[0],&color[1],&color[2],&color[3],&color[4],&color[5],&parameter_1,&parameter_2,&parameter_3);
    new_construct(id,color,parameter_1,parameter_2,parameter_3);
    break;
    
    case 't':
    fscanf(inputFile,"riangle id=\"%d\" color=\"%c%c%c%c%c%c\" ax=\"%d\" ay=\"%d\" bx=\"%d\" by=\"&d\" cx=\"%d\" cy=\"%d\"", &id,&color[0],&color[1],&color[2],&color[3],&color[4],&color[5],&parameter_1,&parameter_2,&parameter_3,&parameter_4,&parameter_5,&parameter_6);
    new_construct(id,color,parameter_1,parameter_2,parameter_3,parameter_4,parameter_5,parameter_6);
    break;
     
  }
  
  if(first_construct == NULL)
  {
    first_construct = new_construct;
  }
  else
  {
    actual_construct = first_construct;
    while(actual_construct->next_construct !=NULL)
    {
      actual_construct = actual_construct->next_construct;
    }
    actual_construct = new_construct;
  }
  

  
  //file close
  
  fclose(inputFile);
  return 0;
  
}
  
  
  
  /*int column = 0;           
  
  char part_of_line[128]; //Max memory access = 128 chars
  
  do
  {
    lines = realloc(lines, (column + 1) * sizeof(char));  //memory new reservation for lines
    for(int linecount = 0; linecount < column + 1; linecount++) 
    {
      lines[linecount] = realloc(lines[linecount], 1 * 128 * sizeof(char));
    }
    fgets (part_of_line, 128, txt);
    strcat(lines[column], part_of_line); //strcat Strings verketten
    
    column++;
  }while(!feof(txt));
  return column;
}
*/
/*
int analysisLines(char **lines, int parametervect[], int column)
{
  char *part_of_line = malloc(300 * sizeof(char));
  char *divider = "/";
  int part_of_line_count = 0;
  int parameter = 1;
  char *color = malloc(7);
  
  if(strstr(lines[column], "rectangle"))  //strstr, string compair
  {
    part_of_line = strtok(lines[column], divider); //strtok, splitt up string
    parametervect[0] = 1;
    while(part_of_line != NULL)
    {
      part_of_line_count++;
      if(part_of_line_count % 2 == 0)
      {
        parametervect[parameter] = atoi(part_of_line);
        parameter++;
        if (parameter == 3)
        {
          color = part_of_line;
        }
        part_of_line = strtok(NULL, divider);
      }
    }
  }
  else if(strstr(lines[column], "circle"))
  {
    part_of_line = strtok(lines[column], divider); //strtok, splitt up string
    parametervect[0] = 2;
    while(part_of_line != NULL)
    {
      part_of_line_count++;
      if(part_of_line_count % 2 == 0)
      {
        parametervect[parameter] = atoi(part_of_line);
        parameter++;
        if (parameter == 3)
        {
          color = part_of_line;
        }
        part_of_line = strtok(NULL, divider);
      }
    }
  }
  else if(strstr(lines[column], "triangle"))
  {
    part_of_line = strtok(lines[column], divider); //strtok, splitt up string
    parametervect[0] = 3;
    while(part_of_line != NULL)
    {
      part_of_line_count++;
      if(part_of_line_count % 2 == 0)
      {
        parametervect[parameter] = atoi(part_of_line);
        parameter++;
        if (parameter == 3)
        {
          color = part_of_line;
        }
        part_of_line = strtok(NULL, divider);
      }
    }
  }
  int numb = (int)strtol(color, NULL, 16);
  free(part_of_line); //deallocates the memory 
  return numb; 
}*/

/*

int appendListElement(int parametervect[], int dye_numb, construct *first_construct);
{
  construct_ *actual_construct;
  
  if(first_construct == NULL)
  {
    first_construct = malloc(sizeof(construct));
    first_construct->type = parametervect[0];
    first_construct->id = parametervect[1];
    first_construct->color = dye_numb;
    first_construct->parameter_1 = parametervect[3];
    first_construct->parameter_2 = parametervect[4];
    first_construct->parameter_3 = parametervect[5];
    first_construct->parameter_4 = parametervect[6];
    first_construct->parameter_5 = parametervect[7];
    first_construct->next_construct = NULL;
    
    printf("Erstes Element erstellt\n");
  }
  else
  {
    actual_construct = first_construct;
    while(actual_construct->next_construct != NULL)
    {
      actual_construct = actual_construct->next_construct;
    }
    
    actual_construct->next_construct = malloc(sizeof(form));
    actual_construct = actual_construct->next_construct;
    
    actual_construct->type = parametervect[0];
    actual_construct->id = parametervect[1];
    actual_construct->color = dye_numb;
    actual_construct->parameter_1 = parametervect[3];
    actual_construct->parameter_2 = parametervect[4];
    actual_construct->parameter_3 = parametervect[5];
    actual_construct->parameter_4 = parametervect[6];
    actual_construct->parameter_5 = parametervect[7];
    actual_construct->next_construct = NULL;
    
    printf("Weiters Element erstellt\n");
  }
  return 0;
}

void printoutList(construct *first_construct)
{
  construct *actual_construct = first_construct;
  printf("Nach diesem Text sollte eine 1 stehen\n");
  
  printf("%d", actual_construct->type);
}

void bootPixels(pixel **pixels, int width, int height)
{
  for(int heightcount = 0; heightcount < height; heightcount++)
  {
    for(int widthcount = 0; widthcount < width; widthcount++)
    {
      pixels[x][y].R = 0xff;
      pixels[x][y].G = 0xff;
      pixels[x][y].B = 0xff;
    }
  }
}

void initBmp(BITMAPFILEHEADER *bmfileh, BITMAPINFOHEADER *bminfoh, int width, int height)
{
  bmfileh->bfType = 0x4D42;
  bmfileh->bfSize = 54 + width * height * 3;
  bmfileh->bfReserved = 0;
  bmfileh->bfOffBits = sizeof(BITMAPFILEHEADER)+sizeof(BITMAPINFOHEADER);
  
  bminfoh->biSize = sizeof(BITMAPINFOHEADER);
  bminfoh->biWidth = width;
  bminfoh->biHeight = height;
  bminfoh->biPlanes = 1;
  bminfoh->biBitCount = 24;
  bminfoh->biCompression = 0;
  bminfoh->biSizeImage = 0;
  bminfoh->biXPelsPerMeter = 0;
  bminfoh->biYPelsPerMeter = 0;
  bminfoh->biClrUsed = 0;
  bminfoh->biClrImportant = 0;
}

int writeBmp(BITMAPFILEHEADER *bmfileh, BITMAPINFOHEADER *bminfoh, char *output, pixel **pixels, int width, int height)
{
    FILE *bmp;
  
  bmp = fopen(output,"wb");
  if(bmp == NULL)
    return 0;
  
  fwrite(bmfileh,sizeof(BITMAPFILEHEADER),1,bmp);
  fwrite(bminfoh,sizeof(BITMAPINFOHEADER),1,bmp);
 
  for(int i = 0; i < height; i++)
  {
    for(int y = 0; y < width; y++)
    {
      fwrite(&pixels[i][y].B, sizeof(uint8_t),1,bmp);
      fwrite(&pixels[i][y].G, sizeof(uint8_t),1,bmp);
      fwrite(&pixels[i][y].R, sizeof(uint8_t),1,bmp);
    } 
    
  }
   
  fclose(bmp);
  
  return 0;
}

void drawRect(char *color, int beginnX, int beginnY, int endX, int endY, pixel **pixels, int width, int height)
{
  int X = 0;
  int Y = 0;
}

*/
