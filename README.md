public class BasicCoffee implements Coffee {

    //Adds topping to the coffee
    @Override
    public void addTopping(Coffee coffee) {

    }
    //Prints name of coffee order, including this topping
    @Override
    public String printCoffee() {
        return "Black coffee";
    }
    //Returns the cost added with the cost of topping
    @Override
    public Double cost() {
        return 0.85;
    }
}
