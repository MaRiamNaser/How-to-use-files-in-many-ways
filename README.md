
#include <iostream>
#include <cstring>
#include <fstream>
using namespace std;
///matensoooooshhh testa5demo el array elli esmo words[] w el 'counter' brdo, da el size bta3 el kalam elli f el file elli 3malnalo load
char words[1000],fileName[80];
int counter=0,whiteSpaces=0;


void displayMenu();
void load(int &i,int &whiteSpaces);///returns counter(the size that you can as the number of times you can loop on the array) and  returns the number of whitespaces(spaces and end lines)
void create();
void display();
void save();
void wordCounter(char arr[],int,int);
int wordSearch(char arr[],int);
void clearFiles();
void Add_More_Data();
void Replace_a_Word();
void Capitalize_Data();
void cnvrtolow(char arr[],int);
void putcontents();
void cipher_decipher(char arr[],int);


int main()
{
    cout<<"Ahlan  Ya User Ya Habibi !!\n actually i hate you !!\n Choose what do you want to do today :\n";

    while (true){
        displayMenu();
        int choose; ///5alloha char and put your numbers in the switch cases as char ('el number')
        cin>>choose;///3aaaaaaa gali elda3't 3bal makt4ft en el error  fi el type bta3 el choose  bs so cute 3matn ^_^ !!

        switch (choose){


            case 1:
                load(counter,whiteSpaces);
                break;
            case 2:
                create();
                break;
            case 3:
                display();
                break;
            case 4:
                save();
                break;
            case 5:
                wordCounter(words,counter,whiteSpaces);
                break;
            case 6:
                wordSearch(words,counter);
                break;
            case 7:
                clearFiles();
                break;
            case 8:
                Add_More_Data();
                break;
            case 9:
                Replace_a_Word();
                break;
            case 10:
                Capitalize_Data();
                break;
            case 11:
                cnvrtolow(words,counter);
            case 12:
                 putcontents();
                break;
            case 13:
                cipher_decipher(words,counter);
                break;
            case 14 :
                return 0;
            default:
                cout<<"please enter a number from 1 to 14";
                break;

        }
    }
    return 0;
}
void displayMenu(){

    cout<<"1- Load an existing file \n" ;
    cout<<"2- Create a new file \n";
    cout<<"3- Display file content\n";
    cout<<"4- Save the loaded text to the same file again or different one \n";
    cout<<"5- Count the words and the characters in the file \n";
    cout<<"6- Search for a word in a file\n";
    cout<<"7- Empty file content\n";
    cout<<"8- Add more content to the end of the file\n";
    cout<<"9- Replace a word in the file with another word\n";
    cout<<"10- Turn all the content file to upper case\n";
    cout<<"11- Turn all the content file to lower case\n";
    cout<<"12- Add another file to the end of the current file\n";
    cout<<"13- Encrypt and decrypt the file\n";
    cout<<"14- End\n\n";
}
void load(int &i,int &whiteSpaces){
    cout<<"enter the name of the file  that  you  want to load : ";

    char fileName[80];
    cin.ignore();
    cin.getline(fileName,80);

    ifstream files(fileName);
    while(files>>noskipws>>words[i]){
        if (words[i]==' '||words[i]=='\n'||words[i]=='.'||words[i]==','||words[i]=='    ')/// 3ndna counter bey3d fee km white space b 2enno yshoof eza el index el folani ==' ' or =='\n'
            ++whiteSpaces;
            ++i;///hena counter tani bei3d howa laf km marra f el loop , y3ni by3d el size bta3 el kalam elli f el file
    }
    if (files.is_open())
    cout<<endl<<" the file is loaded ..!! \n\n ";
    else
        cout<<"the file you want to load is not exist !!"<<endl;

    files.close();
}
void create(){
    cout<<"enter the name of file you want to create :";

    char fileName[81];
    cin.ignore();
    cin.getline(fileName,81);
    ofstream files;
    files.open(fileName);
    cout<<" the file is created !!\n\n";
    files.close();

}
void display(){
    int j=0;
    cout<<"enter the name of the file  that  you  want to display its contents  : ";
    char fileName[80],words2[1000];
    cin.ignore();
    cin.getline(fileName,80);

    ifstream files(fileName);
    while(files>>noskipws>>words2[j]){
        cout<<words2[j]; ///t2reeban nfs el load bl zabt bs el far2 hena bn3l cout henak la2
        ++j;
    }
    cout<<endl<<endl;
    files.close();
}
void save(){/// we will load contents first in an array then we will use this array to print its contents in the new file
    int k=0;
    cout<<"write the name of the file you want to save the contents at:";
    char fileSaveName[80];
    cin.ignore();
    cin.getline(fileSaveName,80);
    cout<<"enter the name of the file  that  you  want to load the contents from: ";
    char fileName[80],words3[1000];
    cin.getline(fileName,80);

    ifstream files(fileName);
    while(files>>noskipws>>words3[k]){
        ++k;
    }
    cout<<endl;
    files.close();
    ofstream files2(fileSaveName);
    for(int j=0;j<k;j++){///3mlna nfs fekret el i (size)
        files2<<words3[j];
    }
    cout<<"contents have been loaded in "<<fileSaveName<<endl<<endl;
    files2.close();

}
void wordCounter(char arr[], int size, int whiteS){
    cout<<"the number of characters in this file is : " << size-whiteS<<endl;
    cout<<"the number of words in this file is : "<<whiteS+1<<endl<<endl;
}

int wordSearch(char arr[],int size ){
    cout<<"enter the word you're searching for : ";
    bool flag=true;
    char word[100];
    int j=0;
    cin.ignore();
    cin>>word;
    for (int k=0;k<size;k++){

        if(arr[k]==' '||arr[k]=='\n'||arr[k]=='.'||arr[k]==','||arr[k+1]=='\0'||arr[k]=='    '){
            //if(word[j+1]!='\0')
              //  flag=false;
            k++;
            j=0;
            if(flag){
                cout<<"Word is found in the file \n\n";
                break;
            }
            else{
                flag=true;
            }
        }
        if(tolower(arr[k])!=tolower(word[j])&&toupper(arr[k])!=toupper(word[j])){
            flag=false;
        }
        j++;
    }
    if (!flag)
    cout<<"Word is not found in the file \n\n";
}

void clearFiles(){
    cout<<"please write the name of the file you want to clear its contents : ";
    char fileName[100];
    cin.ignore();
    cin.getline(fileName,100);

    ofstream files;
    files.open(fileName,ios::out|ios::trunc);

    cout<<"the contents have been cleared."<<endl<<endl;

}
void Add_More_Data()
{
    char fileName[100];
    cout<<"enter the name of the file that you want to add more data to it :";
    cin.ignore();
    cin.getline(fileName,100);
    ofstream files(fileName,ios::app);
    char word[1000];
    cout<<"\n \nenter data  to the end of the file put $ to end :";
    cin.get(word,100,'$');
    cin.ignore();
        for(int i=0;i<strlen(word);i++)
            files<<word[i];
    cout<<"\n \nthe process is done !!\n";
    files.close();
}

void Replace_a_Word()
{

    char wor[100]="";
    char alternate[100]="";

    cout<<"enter the  word you want to replace it:";
    cin>>wor;
    cout<<"enter the word you want to replace with:";
    cin>>alternate;
    string t;
    string x2="";
    string st(words);
    for(int i=0;i<counter;i++)
        {
            t=t+words[i];
            if(t==wor)
         {
            int x=0;
            for(int k=0;k<strlen(alternate);k++)
            {
            //swap(words[i],alternate[x++]);
            //cout<<words[i];
            x2+=alternate[x++];
            }
            t="";
         }

         if((t!=wor)&& (words[i]==' '||i== strlen(words)-1))
         {
          x2+=t;
         t="";
         }
        }cout<<x2<<endl;
}

void Capitalize_Data()
{
    for(int i=0 ;i<strlen(words);i++){
      if (words[i]>=97&&words[i]<=122){
            cout<<char(int(words[i])-32);
            continue;
       }
        cout<<words[i];
    }
    cout<<endl;
}
void cnvrtolow(char arr[] ,int size){
    cin.ignore();
    for (int k=0; k<size ;k++ ){
        if (arr[k]>='A' && arr[k]<='Z')
        {
            cout<<char(arr[k]+ 32);
        }
        else
            cout <<arr[k] ;
        }
        cout<<endl<<endl;
}

void putcontents(){
     cout<<"enter the name of the file you want to add its contents: ";
     char arr;
     char name[80];
     cin>>name;
     ifstream file1;
     file1.open(name);

     char filename[81];
     cout<<"Enter the name of the current file: " ;
     cin>>filename;
     ofstream file2 ;
     file2.open(filename,ios::app);


     while (!file1.eof())
       {
         file1.get(arr);
         file2<<arr;

    }

 }

 void cipher_decipher(char words[],int size){

     cout<<"choose what do you want to do :"<<endl;
     cout<<"1.Cipher"<<endl;
     cout<<"2.Decipher"<<endl;
     int choice ;
     cin>>choice;

     if (choice==1||choice==2){
        string capital ="ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        string small ="abcdefghijklmnopqrstuvwxyz" ;

        for (int l=0 ;l<strlen(words) ;l++){
            if (words[l]>='A' && words[l]<='Z'){
                for (int f=0 ; f<capital.length() ; f++){
                    if (words[l]==capital[f]){
                        words[l]=(capital[(f+13)%26]);

                        break;
                    }
                }
            }
             else {
                for (int f=0 ; f<small.length() ; f++){
                    if (words[l]==small[f]){
                        words[l]=(small[(f+13)%26]);

                        break;
                    }

            }
        }

    }
        cout<<words<<endl<<endl;
    }
 }
