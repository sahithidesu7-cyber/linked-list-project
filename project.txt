#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Song {
    char songName[50];
    struct Song* next;
};

struct Song* head = NULL;

void addSong() {
    struct Song* newSong;
    newSong = (struct Song*)malloc(sizeof(struct Song));

    printf("Enter song name: ");
    scanf(" %[^\n]", newSong->songName);   // Read full line

    newSong->next = NULL;

    if (head == NULL) {
        head = newSong;
        printf("Song added to playlist.\n");
    } else {
        struct Song* temp = head;
        while (temp->next != NULL) {
            temp = temp->next;
        }
        temp->next = newSong;
        printf("Song added to playlist.\n");
    }
}

void deleteSong() {
    if (head == NULL) {
        printf("Playlist is empty. No song to delete.\n");
    } else {
        struct Song* temp = head;
        printf("Deleted song: %s\n", temp->songName);
        head = head->next;
        free(temp);
    }
}

void showPlaylist() {
    if (head == NULL) {
        printf("Playlist is empty.\n");
    } else {
        struct Song* temp = head;
        printf("\nCurrent Playlist:\n");
        while (temp != NULL) {
            printf("- %s\n", temp->songName);
            temp = temp->next;
        }
    }
}

int main() {
    int choice;

    do {
        printf("\n--- MUSIC PLAYLIST MENU ---\n");
        printf("1. Add Song\n");
        printf("2. Delete Song\n");
        printf("3. Show Playlist\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addSong();
                break;

            case 2:
                deleteSong();
                break;

            case 3:
                showPlaylist();
                break;

            case 4:
                printf("Exiting program...\n");
                break;

            default:
                printf("Invalid choice!\n");
        }
    } while (choice != 4);

    return 0;
}
