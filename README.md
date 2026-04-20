/* Name: [SSENYANGE SIMON] 
 Registration Number: [25/U/BIE/11579/PE] 
*/

#include <stdio.h>

int main() {
    // Semester 1 Course Data
    float s1_scores[8];
    int s1_credits[] = {4, 3, 3, 3, 3, 3, 2, 3};
    char* s1_codes[] = {"TEMB 1101", "TEMB 1102", "TEMB 1103", "TEMB 1104", 
                        "TEMB 1105", "TEMB 1106", "TEMB 1107", "TEMB 1108"};
    
    // Semester 2 Course Data
    float s2_scores[8];
    int s2_credits[] = {4, 3, 3, 3, 3, 3, 3, 3};
    char* s2_codes[] = {"TEMB 1201", "TEMB 1202", "TEMB 1203", "TEMB 1204", 
                        "TEMB 1205", "TEMB 1206", "TEMB 1207", "TEMB 1208"};

    float s1_weighted_sum = 0, s2_weighted_sum = 0;
    int s1_total_credits = 0, s2_total_credits = 0;
    float gp, sem1_gpa, sem2_gpa, cgpa;
    char grade;

    // --- Input Semester I ---
    printf("Enter scores for Semester I:\n");
    for (int i = 0; i < 8; i++) {
        printf("%s: ", s1_codes[i]);
        scanf("%f", &s1_scores[i]);
        if (s1_scores[i] < 0 || s1_scores[i] > 100) {
            printf("Invalid score entered\n");
            return 0;
        }
    }

    // --- Input Semester II ---
    printf("\nEnter scores for Semester II:\n");
    for (int i = 0; i < 8; i++) {
        printf("%s: ", s2_codes[i]);
        scanf("%f", &s2_scores[i]);
        if (s2_scores[i] < 0 || s2_scores[i] > 100) {
            printf("Invalid score entered\n");
            return 0;
        }
    }

    printf("\n--- FULL ACADEMIC REPORT ---\n");

    // Process Semester I
    printf("\nSemester I Details:\n");
    for (int i = 0; i < 8; i++) {
        if (s1_scores[i] >= 80) { grade = 'A'; gp = 5.0; }
        else if (s1_scores[i] >= 70) { grade = 'B'; gp = 4.0; }
        else if (s1_scores[i] >= 60) { grade = 'C'; gp = 3.0; }
        else if (s1_scores[i] >= 50) { grade = 'D'; gp = 2.0; }
        else { grade = 'F'; gp = 0.0; }

        float weighted = gp * s1_credits[i];
        s1_weighted_sum += weighted;
        s1_total_credits += s1_credits[i];

        printf("%s | Score: %.1f | Grade: %c | GP: %.1f | CU: %d | Weighted: %.1f\n", 
               s1_codes[i], s1_scores[i], grade, gp, s1_credits[i], weighted);
    }

    // Process Semester II
    printf("\nSemester II Details:\n");
    for (int i = 0; i < 8; i++) {
        if (s2_scores[i] >= 80) { grade = 'A'; gp = 5.0; }
        else if (s2_scores[i] >= 70) { grade = 'B'; gp = 4.0; }
        else if (s2_scores[i] >= 60) { grade = 'C'; gp = 3.0; }
        else if (s2_scores[i] >= 50) { grade = 'D'; gp = 2.0; }
        else { grade = 'F'; gp = 0.0; }

        float weighted = gp * s2_credits[i];
        s2_weighted_sum += weighted;
        s2_total_credits += s2_credits[i];

        printf("%s | Score: %.1f | Grade: %c | GP: %.1f | CU: %d | Weighted: %.1f\n", 
               s2_codes[i], s2_scores[i], grade, gp, s2_credits[i], weighted);
    }

    // Calculations
    sem1_gpa = s1_weighted_sum / s1_total_credits;
    sem2_gpa = s2_weighted_sum / s2_total_credits;
    cgpa = (s1_weighted_sum + s2_weighted_sum) / (s1_total_credits + s2_total_credits);

    // Determine Classification
    char* class;
    if (cgpa >= 4.40) class = "First Class";
    else if (cgpa >= 3.60) class = "Second Class Upper";
    else if (cgpa >= 2.80) class = "Second Class Lower";
    else if (cgpa >= 2.00) class = "Pass";
    else class = "Fail";

    // Summary Output
    printf("\n----------------------------------\n");
    printf("Semester I GPA: %.2f\n", sem1_gpa);
    printf("Semester II GPA: %.2f\n", sem2_gpa);
    printf("CGPA: %.2f\n", cgpa);
    printf("Classification: %s\n", class);
    printf("----------------------------------\n");

    return 0;
}
