#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Room {
    int roomNo;
    char type[30];
    float price;
    int isBooked;   // 0 = Available, 1 = Booked
};

void addRoom();
void displayRooms();
void bookRoom();
void checkIn();
void checkOut();
void cancelBooking();

int main() {
    int choice;

    do {
        printf("\n====== HOTEL ROOM BOOKING SYSTEM ======\n");
        printf("1. Add Room\n");
        printf("2. Display Rooms\n");
        printf("3. Book Room\n");
        printf("4. Check-In\n");
        printf("5. Check-Out\n");
        printf("6. Cancel Booking\n");
        printf("0. Exit\n");
        printf("======================================\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: addRoom(); break;
            case 2: displayRooms(); break;
            case 3: bookRoom(); break;
            case 4: checkIn(); break;
            case 5: checkOut(); break;
            case 6: cancelBooking(); break;
            case 0: printf("Exiting program...\n"); break;
            default: printf("Invalid choice!\n");
        }
    } while (choice != 0);

    return 0;
}

/* ADD ROOM */
void addRoom() {
    FILE *fp;
    struct Room r;

    fp = fopen("rooms.txt", "a");

    printf("Enter Room Number: ");
    scanf("%d", &r.roomNo);
    printf("Enter Room Type: ");
    scanf("%s", r.type);
    printf("Enter Room Price: ");
    scanf("%f", &r.price);

    r.isBooked = 0;

    fprintf(fp, "%d %s %.2f %d\n", r.roomNo, r.type, r.price, r.isBooked);
    fclose(fp);

    printf("Room added successfully!\n");
}

/* DISPLAY ROOMS */
void displayRooms() {
    FILE *fp;
    struct Room r;

    fp = fopen("rooms.txt", "r");
    if (fp == NULL) {
        printf("No rooms available.\n");
        return;
    }

    printf("\nRoomNo  Type      Price     Status\n");
    printf("-----------------------------------\n");

    while (fscanf(fp, "%d %s %f %d",
                  &r.roomNo, r.type, &r.price, &r.isBooked) != EOF) {

        printf("%-7d %-8s %-9.2f %s\n",
               r.roomNo, r.type, r.price,
               r.isBooked ? "Booked" : "Available");
    }

    fclose(fp);
}

/* BOOK ROOM */
void bookRoom() {
    FILE *fp, *temp;
    struct Room r;
    int roomNo, found = 0;

    fp = fopen("rooms.txt", "r");
    temp = fopen("temp.txt", "w");

    if (fp == NULL) {
        printf("No rooms found.\n");
        return;
    }

    printf("Enter Room Number to Book: ");
    scanf("%d", &roomNo);

    while (fscanf(fp, "%d %s %f %d",
                  &r.roomNo, r.type, &r.price, &r.isBooked) != EOF) {

        if (r.roomNo == roomNo && r.isBooked == 0) {
            r.isBooked = 1;
            found = 1;
            printf("Room booked successfully!\n");
        }
        fprintf(temp, "%d %s %.2f %d\n",
                r.roomNo, r.type, r.price, r.isBooked);
    }

    fclose(fp);
    fclose(temp);
    remove("rooms.txt");
    rename("temp.txt", "rooms.txt");

    if (!found)
        printf("Room not available or not found.\n");
}

/* CHECK-IN */
void checkIn() {
    int roomNo;
    char guest[50];

    FILE *fp = fopen("bookings.txt", "a");

    printf("Enter Room Number: ");
    scanf("%d", &roomNo);
    printf("Enter Guest Name: ");
    scanf("%s", guest);

    fprintf(fp, "%d %s\n", roomNo, guest);
    fclose(fp);

    printf("Check-in completed successfully.\n");
}

/* CHECK-OUT */
void checkOut() {
    FILE *fp, *temp;
    struct Room r;
    int roomNo, found = 0;

    fp = fopen("rooms.txt", "r");
    temp = fopen("temp.txt", "w");

    printf("Enter Room Number to Check-Out: ");
    scanf("%d", &roomNo);

    while (fscanf(fp, "%d %s %f %d",
                  &r.roomNo, r.type, &r.price, &r.isBooked) != EOF) {

        if (r.roomNo == roomNo && r.isBooked == 1) {
            r.isBooked = 0;
            found = 1;
            printf("Check-out successful.\n");
        }

        fprintf(temp, "%d %s %.2f %d\n",
                r.roomNo, r.type, r.price, r.isBooked);
    }

    fclose(fp);
    fclose(temp);
    remove("rooms.txt");
    rename("temp.txt", "rooms.txt");

    if (!found)
        printf("Room not found or already available.\n");
}

/* CANCEL BOOKING */
void cancelBooking() {
    FILE *fp, *temp;
    struct Room r;
    int roomNo, found = 0;

    fp = fopen("rooms.txt", "r");
    temp = fopen("temp.txt", "w");

    printf("Enter Room Number to Cancel Booking: ");
    scanf("%d", &roomNo);

    while (fscanf(fp, "%d %s %f %d",
                  &r.roomNo, r.type, &r.price, &r.isBooked) != EOF) {

        if (r.roomNo == roomNo && r.isBooked == 1) {
            r.isBooked = 0;
            found = 1;
            printf("Booking cancelled successfully.\n");
        }

        fprintf(temp, "%d %s %.2f %d\n",
                r.roomNo, r.type, r.price, r.isBooked);
    }

    fclose(fp);
    fclose(temp);
    remove("rooms.txt");
    rename("temp.txt", "rooms.txt");

    if (!found)
        printf("Room not found or already available.\n");
}
