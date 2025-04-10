// TrafficManagementSystem.java

class TrafficSignal {
    private String direction;
    private int vehicleCount;

    public TrafficSignal(String direction, int vehicleCount) {
        this.direction = direction;
        this.vehicleCount = vehicleCount;
    }

    public String getDirection() {
        return direction;
    }

    public int getVehicleCount() {
        return vehicleCount;
    }

    public void setVehicleCount(int vehicleCount) {
        this.vehicleCount = vehicleCount;
    }

    public void allowTraffic(int durationInSeconds) {
        System.out.println("🚦 Green light for " + direction + " (" + durationInSeconds + " seconds)");
        try {
            Thread.sleep(durationInSeconds * 1000L);
        } catch (InterruptedException e) {
            System.out.println("Traffic interrupted for " + direction);
        }
        System.out.println("🔴 Red light for " + direction + "\n");
    }
}

public class TrafficManagementSystem {
    public static void main(String[] args) {
        // Create traffic signals for 4 directions
        TrafficSignal north = new TrafficSignal("North", 10);
        TrafficSignal south = new TrafficSignal("South", 5);
        TrafficSignal east  = new TrafficSignal("East", 15);
        TrafficSignal west  = new TrafficSignal("West", 7);

        // Put signals in array for easy looping
        TrafficSignal[] signals = { north, south, east, west };

        // Simulation loop — runs only once per direction for testing
        for (TrafficSignal signal : signals) {
            int greenTime = calculateGreenTime(signal.getVehicleCount());
            signal.allowTraffic(greenTime);
        }

        System.out.println("✅ Traffic simulation complete.");
    }

    // Calculate green light time based on number of vehicles
    public static int calculateGreenTime(int vehicleCount) {
        int minTime = 5;
        int maxTime = 30;
        int calculatedTime = vehicleCount; // 1 second per vehicle
        return Math.max(minTime, Math.min(calculatedTime, maxTime));
    }
}
