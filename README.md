# Suraj-Assessment
A1. (i) undefined => when we print using console 'a' was not defined
    (ii) undefined => again, when we print using console 'b' was not defined
    (iii) undefined
           10 => before it x was not declared then it was declared
    (iv) compile time error => because there the time was not mentioned after the printing statement

A2. order of execution
        A
        F
        D
        E
        B
        C

B2. interface students { name: string, age: number };

    const student : students = {
    name: "Suraj",
    age: 24
    };

    function getName() {
    return student.name;
    }

    function getAge() {
    return student.age;
    }

    getName();
    getAge();

C2.
        function allSettled(promises) {
            return new Promise((resolve) => {
        const promiseArray = Array.from(promises);
        
        if (promiseArray.length === 0) {
        resolve([]);
        return;
        }

        const results = new Array(promiseArray.length);
        let settledCount = 0;

        promiseArray.forEach((item, index) => {
        Promise.resolve(item)
            .then((value) => {
            results[index] = { status: 'fulfilled', value };
            })
            .catch((reason) => {
            results[index] = { status: 'rejected', reason };
            })
            .finally(() => {
            settledCount++;
            
            if (settledCount === promiseArray.length) {
                resolve(results);
            }
            });
        });
    });
    }
E1.  => RATING COMPONENT
    export class RatingComponent {
    value = model<number>(1);
    stars ='';

    updateRating(rating: number) {
        this.value.set(rating);
    }

    decrement(event: KeyBoardEvent) {
        event.preventDefault();
        const current = this.value();
        if(current>1) {
        this.value.set(current-1);
        }
    }

    increment(event: KeyboardEvent) {
        event.preventDefault();
        const current = this.value();
        if(current<5) {
        this.value.set(current+1);
        }
    }
    }

    => PARENT COMPONENT
    <app-rating [(value)]="parentRatingValue"></app-rating>
    <p>Selected Rating: {{parentRatingValue}}</p>

E2. => (DATASERVICE CLASS) 
    import Injectable
    import HttpClient
    import Observable

    export interface Thing {
    id: number;
    name: string;
    }

    @Injectable({
    providedIn: 'root'
    })

    export class DataService {
    private http = inject(HttpClient);
    private apiUrl = 'https://example.com';

    getThings(): Observable<Thing[]> {
        return this.http.get<Thing[]>(this.apiUrl);
    }
    }

F1. export class TotalComponent {
    price = signal(100);
    qty   = signal(2);
    count = signal(0);
    constructor() {
    // intended: keep a running derived total
    computed(() => { this.count.set(this.count() + 1); });
    // intended: total = price * qty
    this.total = signal(this.price() * this.qty());
    }
    total!: Signal<number>;
    }

F2. zoneless change detection => it was used in older versions, where we need to refresh the components after each update, but since we started using OnPush and signals(), it makes it easy to track any updates or changes made to the components.