/* Name: Ssenyange Simon Peter
   Registration Number: 25/U/BIE/11579/PE */

#include <stdio.h>
#include <stdlib.h>

// Function to get grade point using switch
int getGradePoint(int score) {
    int gp;

    switch(score / 10) {
        case 10:
        case 9:
        case 8:
            gp = 5;
            break;
        case 7:
            gp = 4;
            break;
        case 6:
            gp = 3;
            break;
        case 5:
            gp = 2;
            break;
        default:
            gp = 0;
    }

    return gp;
}

// Function to get grade letter
char getGrade(int score) {
    if(score >= 80) return 'A';
    else if(score >= 70) return 'B';
    else if(score >= 60) return 'C';
    else if(score >= 50) return 'D';
    else return 'F';
}

int main() {

    int scores[16];

    // Credit Units
    int cu_sem1[8] = {4,3,3,3,3,3,2,3};
    int cu_sem2[8] = {4,3,3,3,3,3,3,3};

    int totalCU1 = 0, totalCU2 = 0;
    float totalWP1 = 0, totalWP2 = 0;

    printf("Enter 16 scores:\n");

    for(int i = 0; i < 16; i++) {
        scanf("%d", &scores[i]);

        if(scores[i] < 0 || scores[i] > 100) {
            printf("Invalid score entered");
            return 0;
        }
    }

    // Semester I
    printf("\n--- Semester I ---\n");
    for(int i = 0; i < 8; i++) {
        int gp = getGradePoint(scores[i]);
        char grade = getGrade(scores[i]);
        float wp = gp * cu_sem1[i];

        totalWP1 += wp;
        totalCU1 += cu_sem1[i];

        printf("Course %d | Score: %d | Grade: %c | GP: %d | CU: %d | WP: %.2f\n",
               i+1, scores[i], grade, gp, cu_sem1[i], wp);
    }

    // Semester II
    printf("\n--- Semester II ---\n");
    for(int i = 0; i < 8; i++) {
        int gp = getGradePoint(scores[i+8]);
        char grade = getGrade(scores[i+8]);
        float wp = gp * cu_sem2[i];

        totalWP2 += wp;
        totalCU2 += cu_sem2[i];

        printf("Course %d | Score: %d | Grade: %c | GP: %d | CU: %d | WP: %.2f\n",
               i+9, scores[i+8], grade, gp, cu_sem2[i], wp);
    }

    float gpa1 = totalWP1 / totalCU1;
    float gpa2 = totalWP2 / totalCU2;
    float cgpa = (totalWP1 + totalWP2) / (totalCU1 + totalCU2);

    // Classification
    char classification[30];

    if(cgpa >= 4.40) {
        sprintf(classification, "First Class");
    } else if(cgpa >= 3.60) {
        sprintf(classification, "Second Class Upper");
    } else if(cgpa >= 2.80) {
        sprintf(classification, "Second Class Lower");
    } else if(cgpa >= 2.00) {
        sprintf(classification, "Pass");
    } else {
        sprintf(classification, "Fail");
    }

    // REQUIRED OUTPUT FORMAT
    printf("\nSemester I GPA: %.2f\n", gpa1);
    printf("Semester II GPA: %.2f\n", gpa2);
    printf("CGPA: %.2f\n", cgpa);
    printf("Classification: %s\n", classification);

    return 0;
}
