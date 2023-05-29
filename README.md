# C-Program-to-Find-the-LCM-of-Two-Numbers

LCM of Two Number
The LCM of Two Number num1 and num2 is the smallest positive integer that is perfectly divisible by both num1 and num2 (without a remainder).

LCM_of_two_numbers
Various Method covered
This post explains the following methods – 

Method 1: A linear way to calculate LCM
Method 2: Modified interval Linear way
Method 3: Simple usage of HCF calculation to determine LCM
Method 4: Repeated subtraction to calculate HCF and determine LCM
Method 5: Recursive repeated subtraction to calculate HCF and determine LCM
Method 6: Modulo Recursive repeated subtraction to calculate HCF and determine LCM
Method 1
For a input num1 and num2. This method uses two following observations –

LCM of two numbers will at least be equal or greater than max(num1, num2)
Largest possibility of LCM will be num1 * num2
When iterating in (i) We can linearly find an (i) that is divisible by both num1 & num2

Method 1 Code
Run
#include<stdio.h>

int main()
{
    int num1 = 36, num2 = 60, lcm;

        // finding the larger number here
        int max = (num1 > num2)? num1 : num2;
        
        // LCM will atleast be >= max(num1, num2)
        // Largest possibility of LCM will be num1*num2
        for(int i = max ; i <= num1*num2 ; i++)
        {
            if(i % num1 == 0 && i % num2 == 0){
                lcm = i;
                break;
            }
        }
    
    printf("The LCM: %d", lcm);
    
    return 0;
}
// Time Complexity : O(N)
// Space Complexity : O(1)
Output
The LCM: 180
Method 2
For input num1 and num2. This method uses two following observations –

Rather than linearly checking for LCM by doing i++. We can do i = i + max
Starting with i = max (num1, num2)
The next possibility of LCM will be ‘max’ interval apart
Method 2 Code
Run
#include<stdio.h>

int main()
{
    int num1 = 36, num2 = 60, lcm;

        // finding the larger number here
        int max = (num1 > num2)? num1 : num2;
        
        // can do i++ here
        // but,  i = i + max is done as next possibility of LCM will be
        // max interval apart
        for(int i = max ; i <= num1*num2 ; i=i+max)
        {
            if(i % num1 == 0 && i % num2 == 0){
                lcm = i;
                break;
            }
        }
    
    printf("The LCM: %d", lcm);
    
    return 0;
}
// Time Complexity : O(N)
// Space Complexity : O(1)
Output
The LCM: 180
Method 3
For this method, you need to know how to calculate HCF, check this post here

Main Idea
This method uses the idea that we can calculate the LCM by rather calculating the HCF. As below relationship exist between the two.

LCM * HCF = product of two numbers
LCM * HCF = num1 * num2
Method 3 Code
Run
#include<stdio.h>
int main()
{
    int num1 = 16, num2 = 24, hcf = 1;
    
    // calculating HCF here
    for(int i = 1; i <= num1 || i <= num2; i++) {
        if(num1%i == 0 && num2%i == 0 )
            hcf = i;
    }
    
    // LCM formula
    int lcm = (num1*num2)/hcf;
    
    printf("The LCM: %d", lcm);
    
    return 0;
}
// Time Complexity : O(N)
// Space Complexity : O(1)
Output
The LCM: 48
Method 4
For this method, you need to know how to calculate HCF, check this post here

We use repeated subtraction (Euclidean Algorithm) to calculate the HCF.

Main Idea
Let m = 144, n = 32

m > n
m = m – n = 144 – 32 = 112
now m = 112, n = 32

m = m – n = 112 – 32 = 80
now m = 80, n = 32

m = m – n = 80 – 32 = 48
now m = 48, n = 32

m = m – n = 48 – 32 = 16
now m = 16, n = 32

Since, m < n
We will do subtraction in opposite fashion.

n = n – m = 32 – 16 = 16
now m = 16, n = 16

m = n. So, stop. HCF = 16
Method 4 Code
Run
#include<stdio.h>

int getHCF(int num1, int num2){
    
    // using repeated subtraction here
    while (num1 != num2)
    {
        if (num1 > num2)
            num1 -= num2;
        else
            num2 -= num1;
    }
    
    return num1;
}

int main()
{
    int num1 = 144, num2 = 32;
    
    int hcf = getHCF(num1, num2);
    printf("The HCF: %d\n", hcf);
    
    // LCM formula
    int lcm = (num1*num2)/hcf;
    printf("The LCM: %d", lcm);
    
    return 0;
}
// Time Complexity : O(N)
// Space Complexity : O(1)
Output
The HCF: 16
The LCM: 288
Method 5
This method uses recursion.

For this method, you need to know how to calculate HCF, check this post here

We use repeated subtraction (Euclidean Algorithm) to calculate the HCF.

Main Idea
Previous Codes didn't handle the case when one of the numbers is 0.

The HCF of two numbers by definition when one number is 0, is the other non zero number

Example: HCF of 0 and 6 will be 6
We will handle this case in the below program as well.
Method 5 Code
Run
#include<stdio.h>
// Recursive function for repeated subtraction HCF calculation
int getHCF(int num1, int num2)
{
    // Handles the case when one of the number is 0 (num1) 
    // Check alert above in explanation
    if (num1 == 0)
       return num2;
    
    // Handles the case when one of the number is 0 (num2)
    // Check alert above in explanation
    if (num2 == 0)
       return num1;
  
    // base case
    if (num1 == num2)
        return num1;
  
    // num1 is greater
    if (num1 > num2)
        return getHCF(num1 - num2, num2);

    return getHCF(num1, num2 - num1);
}

int main()
{
    int num1 = 144, num2 = 32;
    
    int hcf = getHCF(num1, num2);
    printf("The HCF: %d\n", hcf);
    
    // LCM formula
    int lcm = (num1*num2)/hcf;
    printf("The LCM: %d", lcm);
    
    return 0;
}
Output
The HCF: 16
The LCM: 288
Method 6
This method uses recursion.

In Addition, we are using modulo operation to reduce the number of subtractions required and improve the time complexity

For this method, you need to know how to calculate HCF, check this post here

We use repeated Modulo Recursive subtraction (Euclidean Algorithm) to calculate the HCF.

Method 6 Code
Run
#include<stdio.h>

// This method improves complexity of repeated substraction
// By efficient use of modulo operator in euclidean algorithm
int getHCF(int a, int b)
{
    return b == 0 ? a : getHCF(b, a % b);   
}

int main()
{
    int num1 = 144, num2 = 32;
    
    int hcf = getHCF(num1, num2);
    printf("The HCF: %d\n", hcf);
    
    // LCM formula
    int lcm = (num1*num2)/hcf;
    printf("The LCM: %d", lcm);
    
    return 0;
}
// Time Complexity: log(max(a,b))
Output
The HCF: 16
The LCM: 288
Prime Course Trailer

Related Banners
Get PrepInsta Prime & get Access to all 200+ courses offered by PrepInsta in One Subscription

Get Prime
