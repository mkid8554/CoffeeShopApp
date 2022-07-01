public abstract class CoffeeDecorator implements Coffee {

    protected Coffee coffee;
    //Constructor
    public CoffeeDecorator(Coffee coffee) {
        this.coffee = coffee;
    }
    //Adds topping to the coffee
    public void addTopping(Coffee coffee) {
        this.coffee.addTopping(coffee);
    }
    //Returns the string containing the full order name
    public String printCoffee() {
        return this.coffee.printCoffee();
    }

    public abstract Double cost();
}
