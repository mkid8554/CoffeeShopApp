public class Milk extends CoffeeDecorator {
    //Constructor
    public Milk(Coffee coffee) {
        super(coffee);
    }

    //Adds topping to the coffee
    @Override
    public void addTopping(Coffee coffee) {
        coffee.addTopping(this.coffee);
        this.coffee = this.coffee;
    }
    //Prints name of coffee order, including this topping
    @Override
    public String printCoffee() {
        return this.coffee.printCoffee() + "-milk";
    }
    //Returns the cost added with the cost of topping
    @Override
    public Double cost() {
        return this.coffee.cost()+0.15;
    }
}
