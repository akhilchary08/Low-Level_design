According to the open-closed principle, software entities should be **open for extension but closed for modification**. The essential concept behind this approach is that we should be able to add new functionality without requiring changes to the existing code:

    class  Triangle {
	public  base: number;
	public  height: number;
	constructor(base: number, height: number) {
		this.base = base;
		this.height = height;
		}
	}
    class  Rectangle {
		public  width: number;
		public  height: number;
		constructor(width: number, height: number) {
			this.width = width;
			this.height = height;
		}
	}
Let’s imagine that we want to develop a function that calculates the area of a collection of shapes.With our current design, it might appear something like the following:

    function  computeAreasOfShapes(
		shapes: Array<Rectangle | Triangle>) {
			return  shapes.reduce(
			(computedArea, shape) => {
				if (shape  instanceof  Rectangle) {
					return  computedArea + shape.width * shape.height;
				}
				if (shape  instanceof  Triangle) {
				return  computedArea + shape.base * shape.height * 0.5 ;}
		},0);
	}
The problem with this method is that every time we add a new shape, we have to change our `computeAreasOfShapes` function, thereby violating the open-closed concept. To demonstrate this, let’s add another shape called `Circle`:

    class  Circle {
		public  radius: number;
		constructor(radius: number) {
			this.radius = radius;
		}
	}
As against the open-closed principle, the `computeAreasOfShapes` function will have to change to a circle instance:
We can solve this issue by enforcing that all of our shapes have a method that returns the area:

    class Triangle implements ShapeAreaInterface {
		public base: number;
		public height: number;
		constructor(base: number, height: number) {
			this.base = base;
			this.height = height;
		}
		public getArea() {
			return this.base * this.height * 0.5
		}
	}
	
	class Rectangle implements ShapeAreaInterface {
		public width: number;
		public height: number;
		constructor(width: number, height: number) {
			this.width = width;
			this.height = height;
		}
		public getArea() {
			return this.width * this.height;
		}
	}
Now that we’re certain that all of our shapes have the `getArea` method, we can utilize it further. From our `computeAreasOfShapes` function, let’s update our code as follows:

    function computeAreasOfShapes(shapes: Shape[]) {
		return shapes.reduce(
			(computedArea, shape) => {
			return computedArea + shape.getArea();
		},0);
	}
Now, we don’t have to change our `computeAreasOfShapes` function every time we add a new shape. You can test this out with the `Circle` shape class. We make it open for extension but closed for modification.
