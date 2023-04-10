#include <stdio.h>
#include <stdlib.h>

#define MAX_REQUESTS 100

struct Request {
    int id;
    int type; // 0 for student, 1 for faculty
    int duration; // duration in seconds
};

int main() {
    // initialize queues
    struct Request student_queue[MAX_REQUESTS];
    int student_front = 0, student_rear = -1, student_size = 0;
    struct Request faculty_queue[MAX_REQUESTS];
    int faculty_front = 0, faculty_rear = -1, faculty_size = 0;

    // initialize time variables
    int start_time = 10 * 60 * 60; // 10am in seconds since midnight
    int end_time = 12 * 60 * 60; // 12pm in seconds since midnight
    int current_time = start_time;
    int total_time = 0;
    int total_queries = 0;

    // loop through time slots
    while (current_time < end_time) {
        // handle student requests
        if (student_size > 0) {
            struct Request request = student_queue[student_front];
            printf("Handling student request %d\n", request.id);
            total_time += request.duration;
            total_queries++;
            student_front = (student_front + 1) % MAX_REQUESTS;
            student_size--;
            current_time += request.duration;
        }
        // handle faculty requests
        else if (faculty_size > 0) {
            struct Request request = faculty_queue[faculty_front];
            printf("Handling faculty request %d\n", request.id);
            total_time += request.duration;
            total_queries++;
            faculty_front = (faculty_front + 1) % MAX_REQUESTS;
            faculty_size--;
            current_time += request.duration;
        }
        // no requests, wait for one second
        else {
            current_time++;
        }

        // add new requests to queues
        if (current_time < end_time) {
            // randomly generate new request
            int request_type = rand() % 2; // 0 for student, 1 for faculty
            int request_duration = rand() % 31 + 30; // 30-60 seconds
            struct Request request = { total_queries + 1, request_type, request_duration };
            if (request_type == 0) {
                if (student_size < MAX_REQUESTS) {
                    student_rear = (student_rear + 1) % MAX_REQUESTS;
                    student_queue[student_rear] = request;
                    student_size++;
                }
            }
            else {
                if (faculty_size < MAX_REQUESTS) {
                    faculty_rear = (faculty_rear + 1) % MAX_REQUESTS;
                    faculty_queue[faculty_rear] = request;
                    faculty_size++;
                }
            }
        }
    }

    // print summary
    printf("Total time spent on handling queries: %d seconds\n", total_time);
    printf("Average query time: %.2f seconds\n", (float)total_time / total_queries);

    return 0;
}
