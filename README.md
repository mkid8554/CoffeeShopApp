
public class WhippedCream extends CoffeeDecorator {

    //Constructor
    public WhippedCream(Coffee coffee) {
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
        //WhippedCream whippedCream;
        if (this.coffee instanceof WhippedCream) {
            return "1";
        } else {
            return this.coffee.printCoffee() + "-whipped cream";
        }
    }
    //Returns the cost added with the cost of topping
    @Override
    public Double cost() {
        if (this.coffee instanceof WhippedCream) {
            return 1.0;
        }
        else{
            return this.coffee.cost() + 0.10;
        }
    }
}
