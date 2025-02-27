#include <iostream>
#include <pthread.h>
#include <queue>
#include <vector>
#include <unistd.h>
#include <algorithm>
#include <mutex>

using namespace std;

struct Process {
    int id, burstTime, priority;
    Process(int i, int bt, int p) : id(i), burstTime(bt), priority(p) {}
};

mutex mtx; // Mutex for thread synchronization

// Comparator for Priority Scheduling
struct ComparePriority {
    bool operator()(Process const &p1, Process const &p2) {
        return p1.priority < p2.priority; // Higher priority executes first
    }
};

void *executeProcess(void *arg) {
    Process *p = (Process *)arg;
    mtx.lock();
    cout << "Executing Process " << p->id << " with burst time " << p->burstTime << "\n";
    sleep(p->burstTime);
    cout << "Process " << p->id << " completed.\n";
    mtx.unlock();
    return nullptr;
}

void FCFS(vector<Process> &processes) {
    for (auto &p : processes) {
        pthread_t thread;
        pthread_create(&thread, nullptr, executeProcess, (void *)&p);
        pthread_join(thread, nullptr);
    }
}

void RoundRobin(vector<Process> &processes, int quantum) {
    queue<Process> q;
    for (auto &p : processes) q.push(p);

    while (!q.empty()) {
        Process p = q.front();
        q.pop();

        int execTime = min(p.burstTime, quantum);
        p.burstTime -= execTime;
        
        pthread_t thread;
        pthread_create(&thread, nullptr, executeProcess, (void *)&p);
        pthread_join(thread, nullptr);

        if (p.burstTime > 0) q.push(p); // Reinsert if still has burst time left
    }
}

void PriorityScheduling(vector<Process> &processes) {
    priority_queue<Process, vector<Process>, ComparePriority> pq;
    for (auto &p : processes) pq.push(p);

    while (!pq.empty()) {
        Process p = pq.top();
        pq.pop();

        pthread_t thread;
        pthread_create(&thread, nullptr, executeProcess, (void *)&p);
        pthread_join(thread, nullptr);
    }
}

int main() {
    vector<Process> processes = {{1, 3, 2}, {2, 2, 1}, {3, 1, 3}};
    int choice;
    cout << "Select Scheduling Algorithm: 1.FCFS 2.Round Robin 3.Priority: ";
    cin >> choice;
    
    if (choice == 1) {
        FCFS(processes);
    } else if (choice == 2) {
        int quantum;
        cout << "Enter time quantum: ";
        cin >> quantum;
        RoundRobin(processes, quantum);
    } else if (choice == 3) {
        PriorityScheduling(processes);
    } else {
        cout << "Invalid choice!";
    }
    return 0;
}
