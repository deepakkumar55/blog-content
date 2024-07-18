---
title: "Building a Secure Employee Dashboard with Facial Authentication: A Comprehensive Next.js Tutorial"
datePublished: Thu Jul 18 2024 14:56:03 GMT+0000 (Coordinated Universal Time)
cuid: clyre8xbu000909l6dbav78mh
slug: building-a-secure-employee-dashboard-with-facial-authentication-a-comprehensive-nextjs-tutorial
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1721314560400/b17fd1a2-8a03-4d21-a34e-fdc4e8e1d2de.png

---

Are you ready to revolutionize your workplace management? In this comprehensive tutorial, we're diving deep into creating a state-of-the-art employee dashboard that leverages facial authentication. We'll be using some of the hottest tools in web development: Next.js, [FACEIO](https://faceio.net/), and Shadcn UI. By the end of this guide, you'll have a sleek, secure dashboard that'll make your employees feel like they're living in the future!

## What You'll Need Before We Start

Before we dive in, let's make sure you've got all your ducks in a row:

- Node.js installed on your machine
- npm or yarn (whichever floats your boat)

Got all that? Great! Let's get this show on the road.

![Faceio Authentication](https://cdn.hashnode.com/res/hashnode/image/upload/v1721314558121/a7255bbd-5b11-4512-bff2-151b079fcbf4.gif)

## Setting Up Your Project: The First Steps

### Step 1: Kickstarting Your Next.js Project

First things first, let's create our Next.js project. Open up your terminal and type in these magic words:

```
npx create-next-app@latest faceio-app
cd faceio-app
```

You'll be asked a few questions. Here's how to answer them:

- TypeScript? Heck yes!
- ESLint? Absolutely!
- Tailwind CSS? You bet!
- src/ directory? Nah, we're good.
- App Router? Yes, please!
- Customize default import alias? We'll pass on this one.

### Step 2: Gathering Your Tools

Now, let's grab all the goodies we need. Run this command to install our dependencies:

```
npm install @faceio/fiojs @shadcn/ui class-variance-authority clsx tailwind-merge
```

### Step 3: Setting Up Your Secret Sauce

Create a file called .env.local in your project's root. This is where we'll keep our secret [FACEIO](https://faceio.net/) app ID:

```
NEXT_PUBLIC_FACEIO_APP_ID=your-super-secret-faceio-app-id
```

Remember to replace 'your-super-secret-faceio-app-id' with your actual [FACEIO](https://faceio.net/) application ID. Keep it safe!

### Step 4: File Structure

Your project structure should look like this:

```
faceio-app/
├── app/
│   ├── layout.tsx
│   ├── page.tsx
│   └── components/
│       ├── FaceAuth.tsx
│       └── EmployeeDashboard.tsx
├── public/
├── .env.local
├── next.config.js
├── package.json
├── tsconfig.json
└── tailwind.config.js
```

### Step 5: Sprucing Up Tailwind CSS

Time to give Tailwind a makeover. Update your tailwind.config.js file with this fancy configuration:

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  darkMode: ["class"],
  content: [
    './app/**/*.{ts,tsx}',
  ],
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: {
        "2xl": "1400px",
      },
    },
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))",
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      keyframes: {
        "accordion-down": {
          from: { height: 0 },
          to: { height: "var(--radix-accordion-content-height)" },
        },
        "accordion-up": {
          from: { height: "var(--radix-accordion-content-height)" },
          to: { height: 0 },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
}
```

## Building the Heart of Your Dashboard

### Step 1: Crafting the FaceAuth Component

Let's create the star of our show - the FaceAuth component. Create a new file app/components/FaceAuth.tsx and paste in this code:

```typescript
import { useEffect } from 'react';
import faceIO from '@faceio/fiojs';
import { Button, Card, CardHeader, CardTitle, CardContent } from '@shadcn/ui';
import { useToast } from '@shadcn/ui';

interface FaceAuthProps {
  onSuccessfulAuth: (data: any) => void;
}

const FaceAuth: React.FC<FaceAuthProps> = ({ onSuccessfulAuth }) => {
  const { toast } = useToast();

  useEffect(() => {
    const faceio = new faceIO(process.env.NEXT_PUBLIC_FACEIO_APP_ID);

    const enrollNewUser = async () => {
      try {
        const userInfo = await faceio.enroll({
          locale: 'auto',
          payload: {
            email: 'employee@example.com',
            pin: '12345',
          },
        });
        toast({
          title: "Success!",
          description: "You're now enrolled in the facial recognition system!",
        });
        console.log('User Enrolled!', userInfo);
      } catch (errCode) {
        toast({
          title: "Oops!",
          description: "Enrollment failed. Please try again.",
          variant: "destructive",
        });
        console.error('Enrollment Failed', errCode);
      }
    };

    const authenticateUser = async () => {
      try {
        const userData = await faceio.authenticate();
        toast({
          title: "Welcome back!",
          description: "Authentication successful.",
        });
        console.log('User Authenticated!', userData);
        onSuccessfulAuth({
          name: 'John Doe',
          position: 'Software Developer',
          department: 'Engineering',
          photoUrl: 'https://example.com/john-doe.jpg',
        });
      } catch (errCode) {
        toast({
          title: "Authentication failed",
          description: "Please try again or enroll.",
          variant: "destructive",
        });
        console.error('Authentication Failed', errCode);
      }
    };

    const enrollBtn = document.getElementById('enroll-btn');
    const authBtn = document.getElementById('auth-btn');
    
    if (enrollBtn) enrollBtn.onclick = enrollNewUser;
    if (authBtn) authBtn.onclick = authenticateUser;

    return () => {
      if (enrollBtn) enrollBtn.onclick = null;
      if (authBtn) authBtn.onclick = null;
    };
  }, [toast, onSuccessfulAuth]);

  return (
    <Card className="w-full max-w-md mx-auto">
      <CardHeader>
        <CardTitle>Facial Authentication</CardTitle>
      </CardHeader>
      <CardContent className="space-y-4">
        <Button id="enroll-btn" variant="outline" className="w-full">
          Enroll New Employee
        </Button>
        <Button id="auth-btn" variant="default" className="w-full">
          Authenticate
        </Button>
      </CardContent>
    </Card>
  );
};

export default FaceAuth;
```

### Step 2: Building the EmployeeDashboard Component

Now, let's create the dashboard that our employees will see. Create app/components/EmployeeDashboard.tsx:

```typescript
import { useState } from 'react';
import { Card, CardHeader, CardTitle, CardContent } from '@shadcn/ui';
import { Button, Avatar, Badge, Table, TableBody, TableCell, TableHead, TableHeader, TableRow } from '@shadcn/ui';
import FaceAuth from './FaceAuth';

interface EmployeeData {
  name: string;
  position: string;
  department: string;
  photoUrl: string;
}

const EmployeeDashboard: React.FC = () => {
  const [isAuthenticated, setIsAuthenticated] = useState(false);
  const [employeeData, setEmployeeData] = useState<EmployeeData | null>(null);

  const handleSuccessfulAuth = (data: EmployeeData) => {
    setIsAuthenticated(true);
    setEmployeeData(data);
  };

  const mockAttendanceData = [
    { date: '2024-07-14', timeIn: '09:00 AM', timeOut: '05:30 PM' },
    { date: '2024-07-13', timeIn: '08:55 AM', timeOut: '05:25 PM' },
    { date: '2024-07-12', timeIn: '09:05 AM', timeOut: '05:35 PM' },
  ];

  return (
    <div className="space-y-6">
      {!isAuthenticated ? (
        <FaceAuth onSuccessfulAuth={handleSuccessfulAuth} />
      ) : (
        <>
          <Card>
            <CardHeader>
              <CardTitle>Employee Profile</CardTitle>
            </CardHeader>
            <CardContent className="flex items-center space-x-4">
              <Avatar className="h-20 w-20" src={employeeData?.photoUrl} alt={employeeData?.name} />
              <div>
                <h2 className="text-2xl font-bold">{employeeData?.name}</h2>
                <p className="text-gray-500">{employeeData?.position}</p>
                <Badge variant="outline">{employeeData?.department}</Badge>
              </div>
            </CardContent>
          </Card>

          <Card>
            <CardHeader>
              <CardTitle>Quick Actions</CardTitle>
            </CardHeader>
            <CardContent className="space-y-4">
              <Button className="w-full">Check-in</Button>
              <Button className="w-full" variant="secondary">Request Leave</Button>
            </CardContent>
          </Card>

          <Card>
            <CardHeader>
              <CardTitle>Attendance Records</CardTitle>
            </CardHeader>
            <CardContent>
              <Table>
                <TableHeader>
                  <TableRow>
                    <TableHead>Date</TableHead>
                    <TableHead>Time In</TableHead>
                    <TableHead>Time Out</TableHead>
                  </TableRow>
                </TableHeader>
                <TableBody>
                  {mockAttendanceData.map((record, index) => (
                    <TableRow key={index}>
                      <TableCell>{record.date}</TableCell>
                      <TableCell>{record.timeIn}</TableCell>
                      <TableCell>{record.timeOut}</TableCell>
                    </TableRow>
                  ))}
                </TableBody>
              </Table>
            </CardContent>
          </Card>
        </>
      )}
    </div>
  );
};

export default EmployeeDashboard;
```

### Step 3: Bringing It All Together

Finally, let's update our main page to show off our hard work. Update app/page.tsx:

```typescript
import EmployeeDashboard from './components/EmployeeDashboard';

export default function Home() {
  return (
    <main className="flex min-h-screen flex-col items-center justify-center p-4">
      <EmployeeDashboard />
    </main>
  );
}
```

Now, let's set up the layout that'll wrap our entire app. Add this code: app/layout.tsx

```typescript
import './globals.css'
import type { Metadata } from 'next'
import { Inter } from 'next/font/google'

const inter = Inter({ subsets: ['latin'] })

export const metadata: Metadata = {
  title: 'Employee Dashboard with Facial Authentication',
  description: 'A cutting-edge employee dashboard featuring facial recognition for secure authentication and efficient workplace management.',
}

export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body className={inter.className}>
        <header className="bg-primary text-white p-4">
          <h1 className="text-2xl font-bold">Faceio Solutions</h1>
        </header>
        <main className="container mx-auto p-4">
          {children}
        </main>
        <footer className="bg-gray-100 text-center p-4 mt-8">
          <p>&copy; 2024 Faceio . All rights reserved.</p>
        </footer>
      </body>
    </html>
  )
}
```

This layout is like the frame of a house - it provides structure for your entire app. It includes a header with your company name, a main content area where your dashboard will appear, and a footer. Plus, it sets up some SEO magic with metadata!

## Key Privacy and Security Practices for FACEIO Integration

### Privacy by Design

- Use access controls, user consent, and opt-out options to protect privacy.

### Meaningful Consent

- Ensure users are aware of data collection.
- Offer freedom of choice and control over their data.
- Allow revocation of consent and data deletion anytime.

### Best Practices

- Obtain clear and appropriate consent, especially for minors.
- Make consent requests easy to find and understand.
- Avoid auto-enrollment and unauthorized enrollments.
- Notify users before collecting biometric data.
- Follow legal data privacy requirements.

### Data Security

- Delete user data upon account deletion.
- Maintain strong data retention and disposal practices.
- Implement and review security safeguards regularly.

For more details, refer to [FACEIO](https://faceio.net/apps-best-practice) Best Practices.

## Key Security Considerations for FACEIO Integration

### Security by Design

- Application security is essential to preserve user trust.
- Follow FACEIO's security best practices to mitigate risks.

### Core Security Features

1. Reject Weak PINs
   - Prevent weak PINs like 0000 or 1234.
   - Default: No.

2. Prevent Duplicate Enrollments
   - Stops users from enrolling multiple times.
   - Default: No.

3. Protect Against Deep-Fakes
   - Detects and blocks spoofing attempts.
   - Default: No.

4. Forbid Minor Enrollments
   - Blocks users under 18 from enrolling.
   - Default: No.

5. Require PIN for Authentication
   - Requires PIN code for each authentication.
   - Default: Yes.

6. Enforce Unique PINs
   - Ensures each user's PIN is unique.
   - Default: No.

7. Ignore Obscured Faces
   - Discards faces under poor lighting or partially masked.
   - Default: Yes.

8. Reject Missing Headers
   - Blocks instantiation without proper HTTP headers.
   - Default: Yes.

9. Restrict Instantiation
   - Limits to specific domains and countries.
   - Default: No.

10. Enable Webhooks
    - Notifies your backend of FACEIO events.
    - Default: No.

For more details, refer to [FACEIO](https://faceio.net/security-best-practice) Security Best Practices.

## Real-World Applications: Where Can You Use This?

Now that we've built this awesome dashboard, you might be wondering, "Where can I use this in the real world?" Well, let me tell you, the possibilities are endless! Here are just a few ideas:

1. Office Management: Say goodbye to old-school punch cards! This system can revolutionize how you track attendance, control access to different areas of your office, and manage employee information.

2. Security Systems: Imagine a world where your office is Fort Knox, but without the hassle. This facial recognition system can be the cornerstone of a robust security protocol.

3. Customer Service Kiosks: Picture this - a customer walks up to a kiosk, it recognizes them instantly, and provides personalized service. It's not science fiction anymore!

## What's Next? The Sky's the Limit!

Congratulations, tech wizard! You've just built a cutting-edge employee dashboard with facial authentication. But why stop here? The beauty of this system is its flexibility. Here are some ideas to take it to the next level:

- Implement real-time notifications for important updates
- Add detailed reporting features for HR
- Integrate with other systems like payroll or project management tools

Remember, in the world of tech, the only limit is your imagination (and maybe your caffeine intake).

So, what do you think? Are you ready to bring your workplace into the future? Give this project a try and let me know how it goes. I'd love to hear about your experiences, any cool features you add, or any challenges you face along the way.

Happy coding, and may your facial recognition never mistake you for your office plant!