https://github.com/omeralpi/shadcn-phone-input/assets/19254700/2f32e063-248f-40e3-8c08-041adf3954be

[Shadcn Phone Input](https://shadcn-phone-input.vercel.app/) is a phone input
component built as part of the Shadcn design system. It offers a blend of
customization and out-of-the-box styling, adhering to Shadcn's sleek and modern
design principles.

## Why

I needed a phone input component for a project. I looked around for any phone
input components that used Shadcn's design system, but I couldn't find any. So,
I decided to make one myself. I hope you find it useful!

## Usage

This component is designed to handle phone inputs in your application. It
includes the option to select a country along with the phone input.

```tsx
import { Button } from "@/components/ui/button";
import {
  Form,
  FormControl,
  FormDescription,
  FormField,
  FormItem,
  FormLabel,
  FormMessage,
} from "@/components/ui/form";
import { PhoneInput } from "@/components/ui/phone-input";
import { toast } from "@/components/ui/use-toast";
import { zodResolver } from "@hookform/resolvers/zod";
import { useForm } from "react-hook-form";
import { isValidPhoneNumber } from "react-phone-number-input";
import { z } from "zod";

const FormSchema = z.object({
  phone: z
    .string()
    .refine(isValidPhoneNumber, { message: "Invalid phone number" }),
});

export default function Hero() {
  const form = useForm<z.infer<typeof FormSchema>>({
    resolver: zodResolver(FormSchema),
  });

  function onSubmit(data: z.infer<typeof FormSchema>) {
    toast({
      title: "You submitted the following values:",
      description: (
        <pre className="mt-2 w-[340px] rounded-md bg-slate-950 p-4">
          <code className="text-white">{JSON.stringify(data, null, 2)}</code>
        </pre>
      ),
    });
  }

  return (
    <Form {...form}>
      <form
        onSubmit={form.handleSubmit(onSubmit)}
        className="space-y-8 flex flex-col items-start">
        <FormField
          control={form.control}
          name="phone"
          render={({ field }) => (
            <FormItem className="flex flex-col items-start">
              <FormLabel className="text-left">Phone Number</FormLabel>
              <FormControl className="w-full">
                <PhoneInput {...field} />
              </FormControl>
              <FormDescription className="text-left">
                Enter a phone number
              </FormDescription>
              <FormMessage />
            </FormItem>
          )}
        />
        <Button type="submit">Submit</Button>
      </form>
    </Form>
  );
}
```

## Documentation

You can find out more about the API and implementation in the
[Documentation](https://shadcn-phone-input.vercel.app/#setup).
