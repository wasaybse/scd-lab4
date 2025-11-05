By using start, stop and sleep methods of threading, print alphabets of English from A-Z. (Hint: use math.random method for getting random numbers and then convert them into characters, print 26 characters under run method loop with fluctuating visualization through sleep method).

    package wasay;
    import java.util.Random;
    public class Wasay extends Thread {
    private volatile boolean running = true; 
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName() + " started printing alphabets...");
               for (int i = 0; i < 26 && running; i++) {
            char alphabet = (char) ('A' + i);
                    Random rand = new Random();
            int sleepTime = rand.nextInt(400) + 100; 

            try {
                
                Thread.sleep(sleepTime);
            } catch (InterruptedException e) {
                System.out.println(Thread.currentThread().getName() + " interrupted: " + e);
                
                Thread.currentThread().interrupt(); 
                return;
            }

            System.out.println(Thread.currentThread().getName() + ": " + alphabet + 
                               " (Slept for " + sleepTime + "ms)");
        }
        System.out.println(Thread.currentThread().getName() + " finished.");
    }

    public void terminate() {
        this.running = false;
    }

    public static void main(String args[]) {
        
        
        Wasay t1 = new Wasay();
        t1.setName("Alphabet-Thread");
        
        
        Wasay t2 = new Wasay();
        t2.setName("Stopper-Thread");

        
        t1.start(); 
        t2.start(); 
        
        
        try {
             
             Thread.sleep(500); 
        } catch (InterruptedException e) {
             
        }

        
        t2.terminate(); 
        System.out.println("\n*** Thread t2 ('Stopper-Thread') requested to stop gracefully using a flag. ***\n");
        
        System.out.println("Main thread continues execution while Alphabet-Thread is running.");
    }
}
