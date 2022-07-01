public class Sugar extends CoffeeDecorator {
    //Constructor
    public Sugar(Coffee coffee) {
        super(coffee);
    }
    //Adds topping to the coffee
    @Override
    public void addTopping(Coffee coffee) {
        coffee.addTopping(this.coffee);
        this.coffee = coffee;
    }
    //Prints name of coffee order, including this topping
    @Override
    public String printCoffee() {
        return this.coffee.printCoffee() + "-sugar";
    }
    //Returns the cost added with the cost of topping
    @Override
    public Double cost() {
        return this.coffee.cost()+0.05;
    }
}
