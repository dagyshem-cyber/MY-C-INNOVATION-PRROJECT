# MY-C-INNOVATION-PRROJECT
#include <stdio.h>
#include <string.h>

#define MAX 100

struct Incident {
    int studentID;
    char device[30];
    char location[30];
    char status[30];
    int riskScore;
};

int main(void) {
    struct Incident incidents[MAX];
    int choice, count = 0, i;
    int deviceChoice, behaviorChoice;
    int risk;

    do {
        printf("\n========================================\n");
        printf(" AI-ASSISTED EXAMINATION INTEGRITY SYSTEM\n");
        printf("========================================\n");
        printf("1. Report suspicious device\n");
        printf("2. View recorded incidents\n");
        printf("3. View examination integrity report\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
        case 1:
            if (count >= MAX) {
                printf("Incident storage is full.\n");
                break;
            }

            risk = 0;

            printf("\nEnter student ID: ");
            scanf("%d", &incidents[count].studentID);

            printf("\nDevice detected:\n");
            printf("1. Smartphone\n");
            printf("2. Smartwatch\n");
            printf("3. Earbuds or other connected device\n");
            printf("4. Other electronic device\n");
            printf("Select device: ");
            scanf("%d", &deviceChoice);

            switch (deviceChoice) {
            case 1:
                strcpy(incidents[count].device, "Smartphone");
                break;
            case 2:
                strcpy(incidents[count].device, "Smartwatch");
                break;
            case 3:
                strcpy(incidents[count].device,
                       "Connected device");
                break;
            case 4:
                strcpy(incidents[count].device,
                       "Other electronic device");
                break;
            default:
                strcpy(incidents[count].device, "Unknown device");
            }

            printf("Enter examination room: ");
            scanf("%29s", incidents[count].location);

            printf("\nObserved situation:\n");
            printf("1. Device permitted or no suspicious activity\n");
            printf("2. Device use during examination\n");
            printf("3. Possible unauthorized communication\n");
            printf("Select observation: ");
            scanf("%d", &behaviorChoice);

            if (behaviorChoice == 2) {
                risk += 40;
            } else if (behaviorChoice == 3) {
                risk += 60;
            }

            if (deviceChoice >= 1 && deviceChoice <= 3) {
                risk += 20;
            }

            if (risk > 100) {
                risk = 100;
            }

            incidents[count].riskScore = risk;

            if (risk >= 60) {
                strcpy(incidents[count].status,
                       "Refer for review");
            } else if (risk >= 40) {
                strcpy(incidents[count].status,
                       "Needs verification");
            } else {
                strcpy(incidents[count].status,
                       "No immediate action");
            }

            printf("\n--- Assessment Result ---\n");
            printf("Device: %s\n",
                   incidents[count].device);
            printf("Risk score: %d/100\n", risk);
            printf("Recommendation: %s\n",
                   incidents[count].status);

            printf("Note: This is a simulated risk score, "
                   "not proof of malpractice.\n");

            count++;
            printf("Incident recorded successfully.\n");
            break;

        case 2:
            if (count == 0) {
                printf("\nNo incidents recorded.\n");
            } else {
                printf("\n--- RECORDED INCIDENTS ---\n");

                for (i = 0; i < count; i++) {
                    printf("\nIncident %d\n", i + 1);
                    printf("Student ID: %d\n",
                           incidents[i].studentID);
                    printf("Device: %s\n",
                           incidents[i].device);
                    printf("Room: %s\n",
                           incidents[i].location);
                    printf("Risk score: %d/100\n",
                           incidents[i].riskScore);
                    printf("Status: %s\n",
                           incidents[i].status);
                }
            }
            break;

        case 3:
            printf("\n--- INTEGRITY REPORT ---\n");
            printf("Total incidents recorded: %d\n", count);

            for (i = 0; i < count; i++) {
                if (incidents[i].riskScore >= 60) {
                    printf("Student %d requires human review.\n",
                           incidents[i].studentID);
                }
            }

            printf("All suspected cases must be reviewed "
                   "by an authorized invigilator.\n");
            break;

        case 4:
            printf("\nExiting the system. Goodbye!\n");
            break;

        default:
            printf("\nInvalid choice. Try again.\n");
        }

    } while (choice != 4);

    return 0;
}
