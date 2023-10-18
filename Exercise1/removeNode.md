```cpp
void deleteNode(Node** head, int position)
{
    Node* temp;
    Node* prev;
    temp = *head;
    prev = *head;

    for (int i = 0; i < position; i++) {
        if (i == 0 && position == 1) {
            *head = (*head)->next;
            free(temp);
        }
        else {
            if (i == position - 1 && temp) {
                prev->next = temp->next;
                free(temp);
            }
            else {
                prev = temp;

                // Position was greater than
                // number of nodes in the list
                if (prev == NULL)


                    break;
                temp = temp->next;
            }
        }
    }
}

/* Function to remove the last node
   of the linked list */
Node* removeLastNode(struct Node* head)
{
    if (head == NULL)
        return NULL;

    if (head->next == NULL) {
        delete head;
        return NULL;
    }

    // Find the second last node
    Node* second_last = head;
    while (second_last->next->next != NULL)
        second_last = second_last->next;

    // Delete last node
    delete (second_last->next);

    // Change next of second last
    second_last->next = NULL;

    return head;
}

/* Function to remove the first node
   of the linked list */
Node* removeFirstNode(struct Node* head)
{
    if (head == NULL)
        return NULL;

    // Move the head pointer to the next node
    Node* temp = head;
    head = head->next;

    delete temp;

    return head;
}
```
