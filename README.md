# recover
recovers jpeg images 
/**
 * recover.c
 *
 * Computer Science 50
 * Problem Set 4
 *
 * Recovers JPEGs from a forensic image.
 */
#include <stdio.h>
#include <stdint.h>
#include <ctype.h>

typedef uint8_t BYTE;


 
int main()
{
    char title[8]; // declare title
    BYTE buffer[512]; // alot the buffer array
    FILE* img = NULL;
    int i=0;

    FILE* file = fopen("card.raw", "r");// open the image
    if (file == NULL)
    {
        printf("Could not open %s.\n", "card.raw");
        return 2;
    }
    
   
   img = fopen(title,"a");// opening a new file
   
    while(fread (&buffer, 512, 1, file) ==1)// checking end of file
    { 
     
    
   fread(&buffer, 512, 1, file);// read the card
   
   // if new jpg found
   if(buffer[0] == 0xff && buffer[1] == 0xd8 && buffer[2] == 0xff && (buffer[3] == 0xe0 || buffer[3] == 0xe1))            
        {
            
              if(fopen(title, "a"))
            {
                fclose(img);// closes the already open file
                sprintf(title,"%.3d.jpg", i); // assigning the name
                img = fopen(title,"a");// opening a new file
                  
                fwrite(&buffer,512,1,img);// writing to the file
                
                i++;// counter increment
            }
                                
        }  
       
    // writing the remaining part of image    
    else if(img!=NULL)
      {      
      
       	 fwrite(&buffer,512,1,img);  
           
      }                     
   // continues to look for jpeg start
      else
      continue;
 }            
            fclose(img);        
            fclose(file);
return 0;  
}
