# Java 8 FAQ's

## What is MetaSpace? How does it differ from PermGen?
- **PremGen:** MetaData information of classes was stored in PremGen (Permanent-Generation) memory type before Java 8. PremGen is **fixed in size** and cannot be dynamically resized. It was a contiguous Java Heap Memory.
- **MetaSpace:** Java 8 stores the MetaData of classes in native memory called **'MetaSpace'**. It is not a contiguous Heap Memory and hence can be **grown dynamically** which helps to overcome the size constraints. This improves the garbage collection, auto-tuning, and de-allocation of metadata.

## What is Optional?
- Wrapper class to check the null values and helps in further processing based on the value.
- It helps avoid NullPointerException by providing a type-level solution for optional values.
- An Optional instance can either contain a non-null value or be empty, indicating the absence of a value. 
- Example:
    ```java     
    import java.util.Optional;

    public class OptionalExample {
        public static void main(String[] args) {
            String text = "Hello";
            Optional<String> optionalText = Optional.of(text);

            // Check if a value is present
            if (optionalText.isPresent()) {
                System.out.println("Value is present: " + optionalText.get());
            }

            // Perform an action if a value is present
            optionalText.ifPresent(value -> System.out.println("Value: " + value));

            // Return a default value if empty
            String valueOrDefault = optionalText.orElse("Default Value");
            System.out.println("Value or default: " + valueOrDefault);

            // Return a value from a supplier if empty
            String valueOrSupplier = optionalText.orElseGet(() -> "Value from Supplier");
            System.out.println("Value or supplier: " + valueOrSupplier);

            // Throw an exception if empty
            try {
                String valueOrThrow = optionalText.orElseThrow(() -> new IllegalArgumentException("Value not found"));
                System.out.println("Value or throw: " + valueOrThrow);
            } catch (IllegalArgumentException e) {
                System.err.println("Exception: " + e.getMessage());
            }

            // Map the value if present
            Optional<String> mappedValue = optionalText.map(String::toUpperCase);
            System.out.println("Mapped value: " + mappedValue.orElse(""));

            // Filter the value if present
            Optional<String> filteredValue = optionalText.filter(v -> v.startsWith("H"));
            System.out.println("Filtered value: " + filteredValue.orElse(""));
        }
    }
    ```