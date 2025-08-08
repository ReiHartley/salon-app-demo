import React from "react";
import { Link, useLocation } from "react-router-dom";
import { createPageUrl } from "@/utils";
import { User } from "@/entities/User";
import { Menu, X, Scissors, Phone, MapPin, Clock } from "lucide-react";
import {
  Sidebar,
  SidebarContent,
  SidebarHeader,
  SidebarProvider,
  SidebarTrigger,
} from "@/components/ui/sidebar";

const navigationItems = [
  { title: "Home", url: createPageUrl("Home") },
  { title: "About", url: createPageUrl("About") },
  { title: "Services", url: createPageUrl("Services") },
  { title: "Booking", url: createPageUrl("Booking") },
  { title: "Gallery", url: createPageUrl("Gallery") },
  { title: "Testimonials", url: createPageUrl("Testimonials") },
  { title: "Contact", url: createPageUrl("Contact") },
];

export default function Layout({ children, currentPageName }) {
  const location = useLocation();
  const [user, setUser] = React.useState(null);

  React.useEffect(() => {
    checkUser();
  }, []);

  const checkUser = async () => {
    try {
      const currentUser = await User.me();
      setUser(currentUser);
    } catch (error) {
      setUser(null);
    }
  };

  const handleLogin = async () => {
    try {
      await User.login();
      await checkUser();
    } catch (error) {
      console.error("Login failed:", error);
    }
  };

  const handleLogout = async () => {
    try {
      await User.logout();
      setUser(null);
    } catch (error) {
      console.error("Logout failed:", error);
    }
  };

  return (
    <SidebarProvider>
      <div className="min-h-screen bg-white flex flex-col">
        <style>{`
          :root {
            --charcoal: #2D2D2D;
            --dark-gray: #4A4A4A;
            --gold: #D4AF37;
            --white: #FFFFFF;
          }
          
          .text-charcoal { color: var(--charcoal); }
          .text-gold { color: var(--gold); }
          .bg-charcoal { background-color: var(--charcoal); }
          .bg-gold { background-color: var(--gold); }
          .border-gold { border-color: var(--gold); }
          .hover\\:bg-gold:hover { background-color: var(--gold); }
          .hover\\:text-gold:hover { color: var(--gold); }
          
          body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
          }
          
          /* Ensure sidebar doesn't overlap content on mobile */
          @media (max-width: 1023px) {
            [data-sidebar="sidebar"] {
              z-index: 60;
            }
          }
        `}</style>

        {/* Desktop Header */}
        <header className="hidden lg:block bg-white sticky top-0 z-50 backdrop-blur-md bg-white/95 shadow-sm">
          <div className="max-w-7xl mx-auto px-6">
            {/* Top bar with logo and controls */}
            <div className="flex items-center justify-between h-20">
              <Link to={createPageUrl("Home")} className="flex items-center gap-3 group">
                <div className="w-10 h-10 bg-charcoal rounded-lg flex items-center justify-center group-hover:bg-gold transition-all duration-300">
                  <Scissors className="w-5 h-5 text-white" />
                </div>
                <div>
                  <h1 className="text-2xl font-bold text-charcoal">Precision Cuts</h1>
                  <p className="text-xs text-gray-500 -mt-1">Barbershop</p>
                </div>
              </Link>

              <div className="flex items-center gap-8">
                <div className="flex items-center gap-2 text-sm text-gray-600">
                  <Phone className="w-4 h-4" />
                  <span className="font-medium whitespace-nowrap">(555) 123-CUTS</span>
                </div>
                
                <div className="flex items-center gap-4">
                  {user && user.role === 'admin' && (
                    <Link
                      to={createPageUrl("AdminDashboard")}
                      className="text-sm font-medium text-gold hover:text-yellow-600 border border-gold px-4 py-2 rounded-lg hover:bg-gold hover:text-charcoal transition-all duration-200 whitespace-nowrap"
                    >
                      Admin
                    </Link>
                  )}
                  
                  {user ? (
                    <div className="flex items-center gap-3">
                      <span className="text-sm text-gray-600 whitespace-nowrap">Hi, {user.full_name.split(' ')[0]}</span>
                      <button
                        onClick={handleLogout}
                        className="text-sm font-medium text-white bg-gray-600 hover:bg-charcoal px-4 py-2 rounded-lg transition-all duration-300 whitespace-nowrap"
                      >
                        Logout
                      </button>
                    </div>
                  ) : (
                    <button
                      onClick={handleLogin}
                      className="text-sm font-medium text-charcoal hover:text-gold px-4 py-2 border border-charcoal rounded-lg hover:bg-charcoal hover:text-white transition-all duration-200 whitespace-nowrap"
                    >
                      Login
                    </button>
                  )}
                </div>
                
                <Link
                  to={createPageUrl("Booking")}
                  className="bg-charcoal hover:bg-gold text-white px-6 py-3 rounded-lg font-medium transition-all duration-300 transform hover:scale-105 whitespace-nowrap"
                >
                  Book Now
                </Link>
              </div>
            </div>
          </div>
          {/* Bottom navigation bar */}
          <div className="border-t border-gray-100">
            <div className="max-w-7xl mx-auto px-6">
              <nav className="flex items-center justify-center h-12 gap-12">
                {navigationItems.map((item) => (
                  <Link
                    key={item.title}
                    to={item.url}
                    className={`text-sm font-medium transition-all duration-200 hover:text-gold whitespace-nowrap ${
                      location.pathname === item.url
                        ? 'text-gold'
                        : 'text-charcoal'
                    }`}
                  >
                    {item.title}
                  </Link>
                ))}
              </nav>
            </div>
          </div>
        </header>

        {/* Mobile Navigation */}
        <Sidebar className="lg:hidden" variant="overlay">
          <SidebarHeader className="border-b border-gray-200 p-6">
            <Link to={createPageUrl("Home")} className="flex items-center gap-3">
              <div className="w-10 h-10 bg-charcoal rounded-lg flex items-center justify-center">
                <Scissors className="w-5 h-5 text-white" />
              </div>
              <div>
                <h2 className="text-xl font-bold text-charcoal">Precision Cuts</h2>
                <p className="text-xs text-gray-500">Barbershop</p>
              </div>
            </Link>
          </SidebarHeader>
          
          <SidebarContent className="p-4">
            <nav className="space-y-2">
              {navigationItems.map((item) => (
                <Link
                  key={item.title}
                  to={item.url}
                  className={`block px-4 py-3 rounded-lg font-medium transition-all duration-200 ${
                    location.pathname === item.url
                      ? 'bg-gold text-white'
                      : 'text-charcoal hover:bg-gray-50 hover:text-gold'
                  }`}
                >
                  {item.title}
                </Link>
              ))}
              {user && user.role === 'admin' && (
                <Link
                  to={createPageUrl("AdminDashboard")}
                  className="block px-4 py-3 rounded-lg font-medium text-gold hover:bg-gold hover:text-white transition-all duration-200 border border-gold"
                >
                  Admin Dashboard
                </Link>
              )}
            </nav>
            
            <div className="mt-8 p-4 bg-gray-50 rounded-lg">
              <div className="flex items-center gap-2 text-sm text-gray-600 mb-2">
                <Phone className="w-4 h-4" />
                <span>(555) 123-CUTS</span>
              </div>
              <div className="flex items-center gap-2 text-sm text-gray-600 mb-4">
                <MapPin className="w-4 h-4" />
                <span>123 Main St, Downtown</span>
              </div>
              <Link
                to={createPageUrl("Booking")}
                className="block w-full text-center bg-charcoal hover:bg-gold text-white px-4 py-2.5 rounded-lg font-medium transition-all duration-300"
              >
                Book Appointment
              </Link>
            </div>
          </SidebarContent>
        </Sidebar>

        {/* Mobile Header */}
        <header className="lg:hidden bg-white border-b border-gray-100 sticky top-0 z-50">
          <div className="flex items-center justify-between p-4">
            <SidebarTrigger className="p-2 hover:bg-gray-100 rounded-lg">
              <Menu className="w-5 h-5" />
            </SidebarTrigger>
            
            <Link to={createPageUrl("Home")} className="flex items-center gap-2">
              <div className="w-8 h-8 bg-charcoal rounded-lg flex items-center justify-center">
                <Scissors className="w-4 h-4 text-white" />
              </div>
              <span className="text-lg font-bold text-charcoal">Precision Cuts</span>
            </Link>
            
            <Link
              to={createPageUrl("Booking")}
              className="bg-charcoal text-white px-4 py-2 rounded-lg text-sm font-medium"
            >
              Book
            </Link>
          </div>
        </header>

        {/* Main Content */}
        <main className="flex-1 relative z-0">
          {children}
        </main>

        {/* Footer */}
        <footer className="bg-charcoal text-white relative z-10">
          <div className="max-w-7xl mx-auto px-6 py-12">
            <div className="grid md:grid-cols-4 gap-8">
              <div className="md:col-span-2">
                <div className="flex items-center gap-3 mb-4">
                  <div className="w-10 h-10 bg-gold rounded-lg flex items-center justify-center">
                    <Scissors className="w-5 h-5 text-charcoal" />
                  </div>
                  <div>
                    <h3 className="text-xl font-bold">Precision Cuts</h3>
                    <p className="text-gray-400 text-sm">Where Sharp Style Starts</p>
                  </div>
                </div>
                <p className="text-gray-300 mb-4 leading-relaxed">
                  Your premier destination for precision haircuts, beard trims, and classic grooming services. 
                  We combine traditional barbering techniques with modern style.
                </p>
              </div>
              
              <div>
                <h4 className="font-semibold mb-4">Contact Info</h4>
                <div className="space-y-3">
                  <div className="flex items-center gap-2 text-gray-300">
                    <Phone className="w-4 h-4" />
                    <span>(555) 123-CUTS</span>
                  </div>
                  <div className="flex items-center gap-2 text-gray-300">
                    <MapPin className="w-4 h-4" />
                    <span>123 Main Street<br />Downtown, ST 12345</span>
                  </div>
                </div>
              </div>
              
              <div>
                <h4 className="font-semibold mb-4">Hours</h4>
                <div className="space-y-2 text-gray-300">
                  <div className="flex justify-between">
                    <span>Mon-Fri</span>
                    <span>9AM-7PM</span>
                  </div>
                  <div className="flex justify-between">
                    <span>Saturday</span>
                    <span>8AM-6PM</span>
                  </div>
                  <div className="flex justify-between">
                    <span>Sunday</span>
                    <span>10AM-4PM</span>
                  </div>
                </div>
              </div>
            </div>
            
            <div className="border-t border-gray-700 mt-8 pt-8 text-center text-gray-400">
              <p>&copy; 2024 Precision Cuts Barbershop. All rights reserved.</p>
            </div>
          </div>
        </footer>
      </div>
    </SidebarProvider>
  );
}
