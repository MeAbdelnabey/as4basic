// FCI – Programming 1 – 2018 - Assignment 4
// Program Name: CS112-2018-2nd –G13&14-20170343-20170364-20170341-A4.cpp
// Last Modification Date: 29/03/2018
// Author1 and ID and Group: Abdelrahman Nasr Abdelsalam Ali    20170343  G13
// Author2 and ID and Group: Yousef Osama Sayed Famhi           20170341  G13
// Author2 and ID and Group: Mohamed Ahmed Abdelnaby   	        20170364  G14
// Teaching Assistant: Mohamed Atta - Ibrahim Zeidan
// Purpose:  image processing software.

#include <iostream>
#include <cstring>
#include "bmplib.cpp"

using namespace std;

unsigned char image[SIZE][SIZE] , image2[SIZE][SIZE] ;

char menu_display();
void load_image(char [100] , unsigned char [SIZE][SIZE]);
void save_image();

void invert_filter();

void rotate_image(string rotate_choice);
void enlarge_image(char sub_choice);

void filter3 ();
void darken_lighten(char sub_choice);
void filter9 ();

int main()
{
    char choice, sub_choice;
    string rotate_choice;

    char loadFile_name[100] , loadFile_name2[100];

    cout << endl << "Please enter file name of the image to process: ";
    cin >> loadFile_name;
    strcat(loadFile_name, ".bmp");
    load_image(loadFile_name , image);

    while(true) {

        choice = menu_display();

        if (choice == '2') invert_filter();

        if (choice == '3') {
            cout << "\tPlease enter name of image file to merge with: ";
            cin >> loadFile_name2 ;strcat(loadFile_name2, ".bmp");
            load_image(loadFile_name2 , image2);

            filter3();
        }

        if (choice == '5'){
            cout << endl << "Do you want to (d)arken or (l)ighten? ";
            cin >> sub_choice;
            cin.ignore();

            darken_lighten(sub_choice);
        }

        if (choice == '6'){
            cout << endl << "Rotate 90, 180 or 270 degrees? ";
            getline(cin, rotate_choice);

            rotate_image(rotate_choice);
        }

        if (choice == '8'){
            cout << endl << "Which quarter to enlarge 1, 2, 3 or 4? ";
            cin >> sub_choice;
            cin.ignore();

            enlarge_image(sub_choice);
        }

        if (choice == '9') {
            filter9();
        }

        if (choice == 's'){
            save_image();
            //load_image(loadFile_name , image);
        }

        if (choice == '0') break;
    }

    return 0;
}

char menu_display() {
    char option;

    cout << endl;
    cout << " =====================================================" << endl;
    cout << " = (1)  Black & White Filter                         =" << endl;
    cout << " = (2)  Invert Filter                                =" << endl;
    cout << " = (3)  Merge Filter                                 =" << endl;
    cout << " = (4)  Flip Image                                   =" << endl;
    cout << " = (5)  Darken and Lighten Image                     =" << endl;
    cout << " = (6)  Rotate Image                                 =" << endl;
    cout << " = (7)  Detect Image Edges                           =" << endl;
    cout << " = (8)  Enlarge Image                                =" << endl;
    cout << " = (9)  Shrink Image                                 =" << endl;
    cout << " = (s)  Save the image to a file                     =" << endl;
    cout << " = (0)  Exit                                         =" << endl;
    cout << " =====================================================" << endl;
    cout << endl;

    cout << "Please select a filter to apply or 0 to exit: ";
    cin >> option;
    cin.ignore();

    return option;
}

void load_image(char loadFile_name[100] , unsigned char image [SIZE][SIZE]) {
    //strcat(loadFile_name, ".bmp");
    readGSBMP(loadFile_name, image);
}

//_______________________________________________________
void save_image() {
    char saveFile_name[100];

    cout << endl << "Please enter target file name: ";
    cin >> saveFile_name;
    strcat(saveFile_name, ".bmp");

    writeGSBMP(saveFile_name, image);
}
//_______________________________________________________
void invert_filter() {
  for (int i=0; i <SIZE; i++) {
    for (int j=0; j <SIZE; j++) {
        image[i][j] = 255 - image[i][j];
    }
  }
}

//_______________________________________________________
void filter3() {
  for (int i = 0; i < SIZE; i++) {
    for (int j = 0; j< SIZE; j++) {
        image[i][j]=(image[i][j] + image2[i][j])/2;
    }
  }
}

//______________________________________________________________
void darken_lighten(char sub_choice) {
    for (int i=0; i <SIZE; i++) {
        for (int j=0; j <SIZE; j++) {
            if (sub_choice == 'd'){
                image[i][j] /= 2;
            }
            if (sub_choice == 'l') {
                image[i][j] /= 2;
                image[i][j] += 128;
            }
        }
  }
}


//____________________________________________
void rotate_image(string rotate_choice) {
    unsigned char new_image[SIZE][SIZE];

    if (rotate_choice == "90") {
        for (int i=0; i <SIZE; i++) {
            for (int j=0; j <SIZE; j++) {
                new_image[255-i][j] = image[j][i];
            }
        }
    }

    if (rotate_choice == "180") {
        for (int i=0; i <SIZE; i++) {
            for (int j=0; j <SIZE; j++) {
                new_image[255-i][255-j] = image[i][j];
            }
        }
    }

    if (rotate_choice == "270") {
        for (int i=0; i <SIZE; i++) {
            for (int j=0; j <SIZE; j++) {
                new_image[i][255-j] = image[j][i];
            }
        }
    }

    for (int i=0; i <SIZE; i++) {
        for (int j=0; j <SIZE; j++) {
            image[i][j] = new_image[i][j];
        }
    }
}

//_______________________________________________________
void enlarge_image(char sub_choice) {
    unsigned char new_image[SIZE+2][SIZE+2];
    int factor_x = 0 , factor_y = 0;

    // factors to access the area required
    if (sub_choice == '2') factor_x = 128;
    if (sub_choice == '3') factor_y = 128;
    if (sub_choice == '4') factor_x = 128, factor_y = 128;

    // taking a quarter of image and scale it into new_image
    for (int i=0; i <SIZE/2 + 1; i++) {
        for (int j=0; j <SIZE/2 + 1; j++) {
            new_image[i*2][j*2] = image[i + factor_y][j + factor_x];
        }
    }

    // get average in every even column from right and left
    for (int i=0; i <SIZE+1; i++) {
        for (int j=0; j <SIZE; j++) {
            if (i%2 == 0 && j%2 != 0) {
                new_image[i][j] = (new_image[i][j-1] + new_image[i][j+1]) / 2;
            }
        }
    }

    // get the average of every odd column from top and bottom
    for (int i=0; i <SIZE; i++) {
        for (int j=0; j <SIZE; j++) {
            if (i%2 != 0) {
                new_image[i][j] = (new_image[i-1][j] + new_image[i+1][j]) / 2;
            }
            // if it is the last column copy the previous column
            if (i == 255) new_image[i][j] = new_image[i-1][j];
        }
    }

    // store the whole quarter new_image into image
    for (int i=0; i <SIZE; i++) {
        for (int j=0; j <SIZE; j++) {
            image[i][j] = new_image[i][j];
        }
    }
}

//_______________________________________________________
void filter9() {
  string choice ; int fac=0;
  cout << "\tShrink to ->> a-(1/2)\tb- (1/3)\tc- (1/4)?   ";
  cin >> choice;
  if (choice == "a" || choice == "A") fac = 2;
  if (choice == "b" || choice == "B") fac = 3;
  if (choice == "c" || choice == "C") fac = 4;
  for (int i=0; i <SIZE; i++) {
        for (int j=0; j <SIZE; j++) {
            image2[i/fac][j/fac] = ( image[i][j+1] + image[i+1][j] ) /2;
            if ( i == 255 ) {
                image2[i/fac][j/fac] = ( image[i][j+1] + image[i][j+1] ) /2;
                if ( j == 255 ) {
                    image2[i/fac][j/fac] = ( image[i-1][j] + image[i][j-1] ) /2;
                }
            }

        }
  }

  for (int i=0; i < SIZE; i++) {
        for (int j=0; j < SIZE; j++) {
            image[i][j]=image2[i][j];
        }
  }

}

