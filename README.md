#include <stdio.h>
#include <math.h>

//Sabbir_Hosen_ Id :- 2018100010063

int main(int argc, char *argv[]) {

    int IP1, IP2, IP3, IP4, CIDR, bitborrowed, bitremained, subnet, host, mask, blocksize;
    char class;

    printf("\n");
    printf("Enter Your IP address Like This 0.0.0.0 \n");
    printf("\n");
    scanf("%i.%i.%i.%i", &IP1, &IP2, &IP3, &IP4);

    //Check if IP is valid
    do
    {
        if((IP1 >255 || IP2 >255 || IP3 >255 || IP4 >255) || (IP1 == 127 || IP1 == 191 || IP1 == 255) || (IP1 == 0 && IP2 == 0 && IP3 == 0 && IP4 == 0))
        {
            printf("\n");
            printf("Oops it's Invalid,Please Enter a valid IP address: |\n");
            printf("\n");
            scanf("%d.%d.%d.%d", &IP1, &IP2, &IP3, &IP4);
        }
    }while((IP1 >255 || IP2 >255 || IP3 >255 || IP4 >255) || (IP1 == 127 || IP1 == 191 || IP1 == 255) || (IP1 == 0 && IP2 == 0 && IP3 == 0 && IP4 == 0));

        //If IP valid ask for netmask
            printf("\n");
            printf("/ Enter Netmask: \n");
            printf("\n");
            scanf("%d", &CIDR);
        do{
            //check if netmask is valid
            if(CIDR > 32 || CIDR == 0)
            {
                printf("\n");
                printf(" Invalid Netmask, Enter a valid Netmask: /\n");
                printf("\n\n");
                scanf("%d", &CIDR);
            }
        }while(CIDR > 32);

    //Let's determine IP class
    if(IP1 <=170) {
        class = 'A';
    }else if(IP1 <=190) {
        class = 'B';
    }else {
        class = 'C';
    }

    //    Let find the number of bits borrowed
    switch (class) {
        case 'A':
            if(CIDR >= 8) {
                bitborrowed = CIDR - 8;
            }else {
                bitborrowed = 8 - CIDR;
            }
            break;
        case 'B':
            if(CIDR >= 16) {
                bitborrowed = CIDR - 16;
            }else {
                bitborrowed = 16 - CIDR;
            }
            break;
        case 'C':
            if(CIDR >= 24) {
                bitborrowed = CIDR - 24;
            }else {
                bitborrowed = 24 -CIDR;
            }
    }

    //Let Find the number of bits that remained
    switch (class) {
        case 'A':
            bitremained = 32 - CIDR;
            break;
        case 'B':
            bitremained = 32 -CIDR;
            break;
        case 'C':
            bitremained = 32 -CIDR;
            break;
    }

    //Now Let Calculate the number of Subnets
    subnet = pow(2,bitborrowed);

    //And then we calculate the number of usable hosts
    host = pow(2, bitremained)-2;

    //Here we determine the block size
    switch(bitborrowed) {
        case 1:
            blocksize = 128;
            break;
        case 2:
            blocksize = 64;
            break;
        case 3:
            blocksize = 32;
            break;
        case 4:
            blocksize = 16;
            break;
        case 5:
            blocksize = 8;
            break;
        case 6:
            blocksize = 4;
            break;
        case 7:
            blocksize = 2;
            break;
        case 8:
            blocksize = 1;
            break;
    }
    printf("\n");
    printf("\n");
    printf("\n\n");
    printf("\n");
    printf("Your IP is %i.%i.%i.%i/%i is of class %c\n", IP1,IP2,IP3,IP4,CIDR,class);
    printf("\n");
    printf("Number of bit borrowed is:\t%d \n", bitborrowed);
    printf("\n");
    printf("Number of bits remained is:\t%d \n", bitremained);
    printf("\n");
    printf("Subnet is:\t%d \n", subnet);
    printf("\n");
    printf("Host is:\t%d \n", host);
    printf("\n");
    printf("blocksize is:\t%d \n", blocksize);
    printf("\n");
    return (0);
}
