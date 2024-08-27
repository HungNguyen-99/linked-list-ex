# linked-list-ex


interface NodeInterface {
    data: string;
    next: NodeInterface | null;
}

class NodeModel implements NodeInterface {
    data: string;
    next: NodeInterface | null;

    constructor(data: string) {
        this.data = data;
        this.next = null;
    }
}

class LinkedList {
    head: NodeInterface | null;
    constructor() {
        this.head = null; // Node đầu tiên của danh sách
    }

    // Phương thức thêm một node vào đầu danh sách
    prepend(data: string) {
        const newNode = new NodeModel(data);
        newNode.next = this.head;
        this.head = newNode;
    }

    // Phương thức thêm một node vào cuối danh sách
    append(data: string) {
        const newNode = new NodeModel(data);
        if (!this.head) {
            this.head = newNode;
            return;
        }
        let current = this.head;
        while (current.next) {
            current = current.next;
        }
        current.next = newNode;
    }

    deleteFirst() {
        if (!this.head) {
            return; // Danh sách rỗng
        }
        this.head = this.head.next;
    }

    deleteLast() {
        if (!this.head || !this.head.next) {
            // Danh sách rỗng hoặc chỉ có một phần tử
            this.head = null;
            return;
        }

        let current = this.head;
        while (current.next?.next) {
            current = current.next;
        }
        current.next = null;
    }

    deleteNode(data: string) {
        let current = this.head;
        console.log('current delete:: ', current);
        let previous = null;

        while (current) {
            console.log('data:: ', current.data);
            if (current.data === data) {
                // Nếu node cần xóa là node đầu
                if (previous === null) {
                    this.head = current.next;
                } else {
                    // Nếu node cần xóa ở giữa hoặc cuối danh sách
                    previous.next = current.next;
                }
                return;
            }
            previous = current;
            current = current.next;
        }
    }

    insertAt(data: string, position: number) {
        if (position < 0) {
            console.error('Invalid position');
            return;
        }

        let newNode = new NodeModel(data);
        let current = this.head;
        let previous = null;
        let count = 0;

        // Duyệt đến vị trí cần chèn
        while (current && count < position) {
            previous = current;
            current = current.next;
            count++;
        }

        // Nếu chèn vào đầu danh sách
        if (previous === null) {
            newNode.next = this.head;
            this.head = newNode;
        } else {
            // Chèn vào giữa hoặc cuối danh sách
            newNode.next = current;
            previous.next = newNode;
        }
    }

    getLength() {
        let count = 0;
        let current = this.head;
        while (current !== null) {
            count++;
            current = current.next;
        }
        return count;
    }

    bubbleSort() {
        let swapped;
        do {
            swapped = false;
            let current: any = this.head;
            while (current?.next !== null) {
                if (current && current.data > current.next.data) {
                    // Đổi chỗ
                    const temp = current.data;
                    current.data = current.next.data;
                    current.next.data = temp;
                    swapped = true;
                }
                current = current?.next;
            }
        } while (swapped);

    }

    reverse() {
        let prev = null;
        let current = this.head;
        while (current !== null) {
            const next = current.next;
            current.next = prev;
            prev = current;
            current = next;

        }
        this.head = prev;

    }

    // Phương thức in ra danh sách
    printList() {
        let current = this.head;
        while (current) {
            console.log(current.data);
            current = current.next;
        }
    }
}

// Tạo một Linked List
const list = new LinkedList();

// Thêm các node vào danh sách
list.append('A');
list.prepend('B');
list.append('C');

list.printList();

console.log('========================');
// list.insertAt('D', 1);
list.reverse();
list.printList();
