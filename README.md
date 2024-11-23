git push -u origin main
'use client'

import { useState, useRef } from 'react'
import { motion, AnimatePresence } from 'framer-motion'
import { ChevronRight, Shirt, Package, Clock, MapPin, Award, ThumbsUp, Users, ChevronDown, Truck, Home, Star, Send, X, Plus, Minus, MessageCircle, Play, Pause, Instagram, Facebook, ArrowLeft, Recycle, Gift, Droplet, AnvilIcon as Iron, Brush, Scissors } from 'lucide-react'

import { Button } from "@/components/ui/button"
import { Textarea } from "@/components/ui/textarea"
import { Dialog, DialogContent, DialogHeader, DialogTitle, DialogDescription, DialogFooter } from "@/components/ui/dialog"
import { Card, CardContent, CardHeader, CardTitle, CardDescription } from "@/components/ui/card"
import { ScrollArea } from "@/components/ui/scroll-area"
import { Input } from "@/components/ui/input"
import { Label } from "@/components/ui/label"

const TikTokIcon = ({ className }: { className?: string }) => (
  <svg className={className} fill="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
    <path d="M19.59 6.69a4.83 4.83 0 0 1-3.77-4.25V2h-3.45v13.67a2.89 2.89 0 0 1-5.2 1.74 2.89 2.89 0 0 1 2.31-4.64 2.93 2.93 0 0 1 .88.13V9.4a6.84 6.84 0 0 0-1-.05A6.33 6.33 0 0 0 5 20.1a6.34 6.34 0 0 0 10.86-4.43v-7a8.16 8.16 0 0 0 4.77 1.52v-3.4a4.85 4.85 0 0 1-1-.1z"/>
  </svg>
)

const services = [
  {
    title: 'Lavado y Planchado de Lujo',
    description: 'Tratamiento premium para tus prendas más delicadas.',
    price: 'Desde $150',
    icon: Iron,
  },
  {
    title: 'Tintorería Especializada',
    description: 'Cuidado experto para tus prendas de color.',
    price: 'Desde $200',
    icon: Droplet,
  },
  {
    title: 'Limpieza en Seco Avanzada',
    description: 'Tecnología de punta para tus prendas más exigentes.',
    price: 'Desde $250',
    icon: Brush,
  },
  {
    title: 'Restauración de Prendas',
    description: 'Devolvemos la vida a tus prendas favoritas.',
    price: 'Desde $300',
    icon: Scissors,
  },
  {
    title: 'Limpieza de Artículos del Hogar',
    description: 'Desde cortinas hasta alfombras, lo cuidamos todo.',
    price: 'Desde $400',
    icon: Home,
  }
]

const serviceProducts = {
  'Lavado y Planchado de Lujo': [
    { name: 'Camisa', price: 50 },
    { name: 'Pantalón', price: 60 },
    { name: 'Vestido', price: 80 },
    { name: 'Traje', price: 150 },
  ],
  'Tintorería Especializada': [
    { name: 'Prenda de seda', price: 100 },
    { name: 'Prenda de lana', price: 120 },
    { name: 'Prenda de cuero', price: 200 },
  ],
  'Limpieza en Seco Avanzada': [
    { name: 'Abrigo', price: 180 },
    { name: 'Chaqueta', price: 150 },
    { name: 'Corbata', price: 40 },
  ],
  'Restauración de Prendas': [
    { name: 'Reparación simple', price: 100 },
    { name: 'Reparación compleja', price: 200 },
    { name: 'Restauración de color', price: 150 },
  ],
  'Limpieza de Artículos del Hogar': [
    { name: 'Cortina (por panel)', price: 120 },
    { name: 'Alfombra (por m²)', price: 80 },
    { name: 'Tapicería de sofá', price: 250 },
  ],
};

const serviceTechniques = {
  'Lavado y Planchado de Lujo': [
    {
      title: 'Clasificación Experta',
      description: 'Separamos meticulosamente cada prenda según su tipo de tela, color y nivel de suciedad.',
      tip: 'Separa siempre tus prendas blancas de las de color para mantener su brillo.'
    },
    {
      title: 'Pretatamiento de Manchas',
      description: 'Aplicamos tratamientos específicos para cada tipo de mancha antes del lavado principal.',
      tip: 'Trata las manchas lo antes posible para evitar que se fijen en la tela.'
    },
    {
      title: 'Lavado Delicado',
      description: 'Utilizamos detergentes de alta calidad y programas de lavado adaptados a cada tipo de prenda.',
      tip: 'Lee siempre las etiquetas de cuidado de tus prendas para conocer la temperatura de lavado adecuada.'
    },
    {
      title: 'Secado Controlado',
      description: 'Secamos tus prendas a la temperatura óptima para evitar encogimientos y deformaciones.',
      tip: 'Evita secar al sol directo las prendas de colores vivos para prevenir su decoloración.'
    },
    {
      title: 'Planchado Profesional',
      description: 'Utilizamos técnicas avanzadas de planchado para un acabado impecable sin dañar las fibras.',
      tip: 'Plancha las prendas de adentro hacia afuera para evitar brillos indeseados en la tela.'
    }
  ],
  'Tintorería Especializada': [
    {
      title: 'Análisis de Fibras',
      description: 'Examinamos detalladamente la composición de cada prenda para determinar el mejor tratamiento.',
      tip: 'Conoce la composición de tus prendas para elegir el método de limpieza más adecuado.'
    },
    {
      title: 'Prueba de Solidez del Color',
      description: 'Realizamos pruebas para asegurar que los colores no se destiñan durante el proceso de limpieza.',
      tip: 'Lava las prendas nuevas por separado las primeras veces para evitar transferencias de color.'
    },
    {
      title: 'Limpieza Especializada',
      description: 'Utilizamos solventes y técnicas específicas para cada tipo de tela y color.',
      tip: 'Evita el uso de blanqueadores en prendas de color, ya que pueden dañar los tintes.'
    },
    {
      title: 'Tratamiento de Protección',
      description: 'Aplicamos productos que ayudan a mantener la intensidad del color y protegen contra manchas futuras.',
      tip: 'Guarda tus prendas de color lejos de la luz directa del sol para preservar su viveza.'
    },
    {
      title: 'Acabado Profesional',
      description: 'Realizamos un planchado y acabado cuidadoso para resaltar los colores y texturas de cada prenda.',
      tip: 'Voltea las prendas de color antes de plancharlas para evitar brillos y proteger los estampados.'
    }
  ],
  'Limpieza en Seco Avanzada': [
    {
      title: 'Inspección Inicial',
      description: 'Examinamos cada prenda en busca de manchas, daños o áreas que requieran atención especial.',
      tip: 'Revisa tus prendas antes de guardarlas para tratar cualquier mancha lo antes posible.'
    },
    {
      title: 'Pretratamiento de Manchas',
      description: 'Aplicamos agentes especializados para tratar manchas difíciles antes del proceso principal.',
      tip: 'No frotes las manchas agresivamente, ya que esto puede extenderlas o dañar la tela.'
    },
    {
      title: 'Limpieza con Solventes Ecológicos',
      description: 'Utilizamos solventes de última generación que son efectivos y respetuosos con el medio ambiente.',
      tip: 'Opta por servicios de limpieza en seco que utilicen solventes ecológicos para reducir el impacto ambiental.'
    },
    {
      title: 'Ciclo de Limpieza Controlado',
      description: 'Monitoreamos cuidadosamente la temperatura y duración del ciclo para un resultado óptimo.',
      tip: 'Sigue siempre las instrucciones de la etiqueta sobre si una prenda puede limpiarse en seco.'
    },
    {
      title: 'Proceso de Finalización',
      description: 'Realizamos un acabado profesional, incluyendo planchado y eliminación de pelusas.',
      tip: 'Guarda tus prendas limpias en seco en fundas transpirables para mantenerlas en óptimas condiciones.'
    }
  ],
  'Restauración de Prendas': [
    {
      title: 'Tratamiento de Manchas Difíciles',
      description: 'Aplicamos métodos especializados para eliminar manchas persistentes sin dañar el tejido.',
      tip: 'Trata las manchas lo antes posible para evitar que se fijen en la tela.'
    },
    {
      title: 'Restauración de Color',
      description: 'Utilizamos tintes especiales para revivir colores desvanecidos en prendas desgastadas.',
      tip: 'Lava las prendas de color del revés para minimizar la decoloración.'
    },
    {
      title: 'Remodelación de Prendas',
      description: 'Ofrecemos servicios de ajuste y remodelación para actualizar el estilo de prendas antiguas.',
      tip: 'Considera remodelar prendas que ya no uses en lugar de desecharlas.'
    }
  ],
  'Limpieza de Artículos del Hogar': [
    {
      title: 'Limpieza de Cortinas',
      description: 'Utilizamos técnicas especializadas para limpiar y restaurar cortinas de diversos materiales.',
      tip: 'Aspira regularmente tus cortinas para evitar la acumulación de polvo y alérgenos.'
    },
    {
      title: 'Lavado de Alfombras y Tapetes',
      description: 'Aplicamos métodos de limpieza profunda para eliminar manchas y olores de alfombras y tapetes.',
      tip: 'Rota tus alfombras periódicamente para distribuir el desgaste de manera uniforme.'
    },
    {
      title: 'Cuidado de Tapicería',
      description: 'Limpiamos y restauramos muebles tapizados, devolviendo su frescura y apariencia original.',
      tip: 'Aspira tu tapicería semanalmente para prevenir que la suciedad se incruste en las fibras.'
    },
    {
      title: 'Tratamiento de Ropa de Cama',
      description: 'Ofrecemos un cuidado especial para sábanas, edredones y almohadas, asegurando una limpieza higiénica.',
      tip: 'Lava tu ropa de cama cada 1-2 semanas para mantener un ambiente de descanso saludable.'
    },
    {
      title: 'Limpieza de Artículos Decorativos',
      description: 'Cuidamos de tus cojines decorativos, manteles y otros textiles del hogar con atención al detalle.',
      tip: 'Rota tus cojines decorativos regularmente para mantener su forma y distribuir el desgaste.'
    }
  ]
}

const recyclingTips = [
  {
    title: 'Reutilización Creativa',
    description: 'Transforma prendas viejas en nuevos artículos como bolsas de compras, fundas de almohadas o trapos de limpieza.',
    icon: Recycle
  },
  {
    title: 'Donación a Fundaciones',
    description: 'Dona ropa en buen estado a organizaciones benéficas locales que apoyan a personas necesitadas.',
    icon: Gift
  },
  {
    title: 'Reciclaje Textil',
    description: 'Lleva las prendas que ya no sirven a centros de reciclaje textil para que sean procesadas y reutilizadas.',
    icon: Recycle
  }
]

const reviews = [
  { name: 'María L.', rating: 5, comment: 'Excelente servicio. Mis prendas quedaron impecables y el proceso fue muy conveniente.' },
  { name: 'Carlos R.', rating: 4, comment: 'Muy buen servicio. La entrega fue puntual y la calidad del lavado superó mis expectativas.' },
  { name: 'Ana S.', rating: 5, comment: 'Increíble atención al cliente. Resolvieron todas mis dudas y el resultado fue perfecto.' }
]

const steps = [
  { 
    icon: Shirt, 
    title: 'Selecciona tus prendas',
    description: 'Elige las prendas que necesitas lavar o tratar. Nuestro sistema inteligente te guiará para asegurar el mejor cuidado para cada tipo de prenda.'
  },
  { 
    icon: MapPin, 
    title: 'Indica la dirección',
    description: 'Proporciona la dirección para la recolección. Puedes guardar múltiples direcciones para mayor comodidad en futuros pedidos.'
  },
  { 
    icon: Truck, 
    title: 'Recolección y proceso',
    description: 'Nuestro equipo recogerá tus prendas en la fecha y hora que elijas. Las trataremos con el máximo cuidado y atención a los detalles.'
  },
  { 
    icon: Home, 
    title: 'Entrega personalizada',
    description: 'Una vez listas, te entregaremos tus prendas en la dirección que prefieras. Puedes configurar una dirección diferente para la entrega si lo deseas.'
  }
]

export default function HomePage() {
  const [isServicesOpen, setIsServicesOpen] = useState(false)
  const [isHowItWorksOpen, setIsHowItWorksOpen] = useState(false)
  const [newReview, setNewReview] = useState('')
  const [isServiceModalOpen, setIsServiceModalOpen] = useState(false)
  const [currentService, setCurrentService] = useState('')
  const [isVideoPlaying, setIsVideoPlaying] = useState(true)
  const [isOrderModalOpen, setIsOrderModalOpen] = useState(false)
  const [selectedProducts, setSelectedProducts] = useState<{[key: string]: number}>({});
  const [selectedService, setSelectedService] = useState('');
  const videoRef = useRef<HTMLVideoElement>(null)

  const handleServiceClick = (serviceTitle: string) => {
    setIsServicesOpen(false)
    setCurrentService(serviceTitle)
    setIsServiceModalOpen(true)
  }

  const handleHowItWorksClick = (event: React.MouseEvent<HTMLAnchorElement>) => {
    event.preventDefault()
    setIsHowItWorksOpen(prev => !prev)
    setTimeout(() => {
      const element = document.getElementById('como-funciona')
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' })
      }
    }, 100)
  }

  const handleSmoothScroll = (event: React.MouseEvent<HTMLAnchorElement>, id: string) => {
    event.preventDefault()
    const element = document.getElementById(id)
    if (element) {
      element.scrollIntoView({ behavior: 'smooth' })
    }
  }

  const handleSubmitReview = (event: React.FormEvent) => {
    event.preventDefault()
    console.log('Nueva reseña:', newReview)
    setNewReview('')
    alert('¡Gracias por tu reseña!')
  }

  const toggleVideo = () => {
    if (videoRef.current) {
      if (isVideoPlaying) {
        videoRef.current.pause()
      } else {
        videoRef.current.play()
      }
      setIsVideoPlaying(!isVideoPlaying)
    }
  }

  const handleVideoError = () => {
    if (videoRef.current) {
      videoRef.current.style.display = 'none'
      const fallbackImage = document.querySelector('img[alt="Fondo de lavandería"]') as HTMLImageElement
      if (fallbackImage) {
        fallbackImage.style.display = 'block'
      }
    }
  }

  const handleOrderButtonClick = () => {
    setIsOrderModalOpen(true)
  }

  const handleOrderSubmit = (event: React.FormEvent<HTMLFormElement>) => {
    event.preventDefault();
    const formData = new FormData(event.currentTarget);
    const orderDetails = {
      name: formData.get('name'),
      email: formData.get('email'),
      phone: formData.get('phone'),
      address: formData.get('address'),
      service: selectedService,
      products: Object.entries(selectedProducts)
        .filter(([_, quantity]) => quantity > 0)
        .map(([name, quantity]) => {
          const price = serviceProducts[selectedService as keyof typeof serviceProducts]
            .find(p => p.name === name)?.price || 0;
          return `${name} (x${quantity}) - $${price * quantity}`;
        })
        .join(', '),
    };
    console.log('Pedido enviado:', orderDetails);
    setIsOrderModalOpen(false);
    setSelectedService('');
    setSelectedProducts({});
    alert('¡Gracias por tu pedido! Nos pondremos en contacto contigo pronto.');
  };

  return (
    <div className="min-h-screen bg-gradient-to-b from-blue-100 to-white">
      {/* Header */}
      <header className="container mx-auto px-4 py-6 flex flex-col md:flex-row justify-between items-center bg-white bg-opacity-80 sticky top-0 z-50">
        <div className="flex items-center mb-4 md:mb-0">
          <h1 className="text-3xl font-bold text-blue-600">Cuidado Infinito</h1>
          <span className="ml-2 text-sm font-medium text-blue-500">30 Años de Excelencia</span>
        </div>
        <nav>
          <ul className="flex flex-wrap justify-center space-x-4 md:space-x-6">
            <li className="relative">
              <button
                onClick={() => setIsServicesOpen(!isServicesOpen)}
                className="text-blue-600 hover:text-blue-800 flex items-center"
                aria-expanded={isServicesOpen}
                aria-haspopup="true"
              >
                Servicios
                <ChevronDown className="ml-1 h-4 w-4" />
              </button>
              <AnimatePresence>
                {isServicesOpen && (
                  <motion.div
                    initial={{ opacity: 0, y: -10 }}
                    animate={{ opacity: 1, y: 0 }}
                    exit={{ opacity: 0, y: -10 }}
                    transition={{ duration: 0.2 }}
                    className="absolute z-10 mt-2 w-56 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5"
                  >
                    <div className="py-1" role="menu" aria-orientation="vertical">
                      {services.map((service, index) => (
                        <button
                          key={index}
                          className="block w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-blue-100"
                          role="menuitem"
                          onClick={() => handleServiceClick(service.title)}
                        >
                          {service.title}
                        </button>
                      ))}
                    </div>
                  </motion.div>
                )}
              </AnimatePresence>
            </li>
            <li>
              <a
                href="#como-funciona"
                className="text-blue-600 hover:text-blue-800"
                onClick={handleHowItWorksClick}
              >
                Cómo funciona
              </a>
            </li>
            <li>
              <a
                href="#experiencia"
                className="text-blue-600 hover:text-blue-800"
                onClick={(e) => handleSmoothScroll(e, 'experiencia')}
              >
                Nuestra Experiencia
              </a>
            </li>
            <li>
              <a
                href="#contacto"
                className="text-blue-600 hover:text-blue-800"
                onClick={(e) => handleSmoothScroll(e, 'contacto')}
              >
                Contacto
              </a>
            </li>
          </ul>
        </nav>
      </header>

      <main>
        {/* Hero Section */}
        <section className="relative h-screen flex items-center justify-center overflow-hidden">
          <video
            ref={videoRef}
            autoPlay
            loop
            muted
            playsInline
            className="absolute w-full h-full object-cover"
            onError={handleVideoError}
          >
            <source src="https://hebbkx1anhila5yf.public.blob.vercel-storage.com/487507_Self%20Service%20Laundry%20Laundromat%20Washing%20Machine%20Clothes_By_Seffy_(Joseph)_Hirsch_Artlist_HD-3UlyUe37i2AjDMxxZ3u5tE8JXaYpi7.mp4" type="video/mp4" />
            Tu navegador no soporta el elemento de video.
          </video>
          <div className="absolute inset-0 bg-black bg-opacity-50"></div>
          <img
            src="/placeholder.svg?height=1080&width=1920"
            alt="Fondo de lavandería"
            className="absolute w-full h-full object-cover hidden"
          />
          <div className="relative z-10 text-center text-white">
            <h2 className="text-5xl font-bold mb-4">Cuidado Infinito para tu Ropa</h2>
            <p className="text-xl mb-8">30 años cuidando tu ropa con la dedicación que mereces</p>
            <div className="flex flex-col sm:flex-row justify-center items-center gap-4">
              <Button size="lg" className="bg-blue-600 hover:bg-blue-700 text-white" onClick={handleOrderButtonClick}>
                Experimenta nuestro servicio ahora
                <ChevronRight className="ml-2 h-4 w-4" />
              </Button>
              <Button 
                variant="outline" 
                size="lg" 
                className="bg-white text-blue-600 border-blue-600 hover:bg-blue-50"
                onClick={() => window.open('https://wa.me/5543746359', '_blank')}
              >
                <MessageCircle className="mr-2 h-5 w-5" />
                Chatea con nosotros en WhatsApp
              </Button>
            </div>
          </div>
          <Button
            variant="outline"
            size="icon"
            className="absolute bottom-4 right-4 bg-white bg-opacity-50 hover:bg-opacity-75"
            onClick={toggleVideo}
          >
            {isVideoPlaying ? <Pause className="h-4 w-4" /> : <Play className="h-4 w-4" />}
          </Button>
        </section>

        {/* How it Works Section */}
        <section id="como-funciona" className="container mx-auto px-4 py-16 scroll-mt-20">
          <h3 className="text-3xl font-semibold mb-6 text-center">Cómo funciona</h3>
          <AnimatePresence>
            {isHowItWorksOpen && (
              <motion.div
                initial={{ opacity: 0, height: 0 }}
                animate={{ opacity: 1, height: 'auto' }}
                exit={{ opacity: 0, height: 0 }}
                transition={{ duration: 0.3 }}
              >
                <p className="text-center mb-8 max-w-2xl mx-auto">
                  En Cuidado Infinito, hemos simplificado el proceso de cuidado de tu ropa para brindarte una experiencia sin complicaciones. Nuestro servicio está diseñado para adaptarse a tu estilo de vida ocupado, ofreciéndote comodidad y flexibilidad en cada paso.
                </p>
              </motion.div>
            )}
          </AnimatePresence>
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
            {steps.map((step, index) => (
              <motion.div
                key={index}
                className="p-6 rounded-lg shadow-lg bg-white"
                whileHover={{ scale: 1.05 }}
              >
                <step.icon className="w-12 h-12 mx-auto mb-4 text-blue-600" />
                <h4 className="text-lg font-semibold mb-2 text-center">{step.title}</h4>
                <p className="text-sm text-center">{step.description}</p>
              </motion.div>
            ))}
          </div>
        </section>

        {/* Customer Experience Section */}
        <section id="experiencia" className="container mx-auto px-4 py-16 bg-gray-50">
          <h3 className="text-3xl font-semibold mb-6 text-center">Experiencias de Nuestros Clientes</h3>
          <div className="grid grid-cols-1 md:grid-cols-3 gap-8 mb-8">
            {reviews.map((review, index) => (
              <motion.div
                key={index}
                className="p-6 bg-white rounded-lg shadow-lg"
                whileHover={{ scale: 1.05 }}
              >
                <div className="flex items-center mb-2">
                  {[...Array(review.rating)].map((_, i) => (
                    <Star key={i} className="w-5 h-5 text-yellow-400 fill-current" />
                  ))}
                </div>
                <p className="mb-2 italic">"{review.comment}"</p>
                <p className="text-right text-sm text-gray-600">- {review.name}</p>
              </motion.div>
            ))}
          </div>
          <div className="max-w-md mx-auto">
            <h4 className="text-xl font-semibold mb-4 text-center">Comparte tu experiencia</h4>
            <form onSubmit={handleSubmitReview}>
              <Textarea
                placeholder="Cuéntanos sobre tu experiencia con Cuidado Infinito..."
                value={newReview}
                onChange={(e) => setNewReview(e.target.value)}
                className="mb-4"
                rows={4}
              />
              <Button type="submit" className="w-full bg-blue-600 hover:bg-blue-700 text-white">
                Enviar reseña
                <Send className="ml-2 h-4 w-4" />
              </Button>
            </form>
          </div>
        </section>

        {/* Contact Section */}
        <section id="contacto" className="bg-blue-600 text-white py-16">
          <div className="container mx-auto px-4 text-center">
            <h3 className="text-3xl font-semibold mb-6">Contáctanos</h3>
            <p className="mb-4">¿Tienes alguna pregunta? Nuestro equipo experto está aquí para ayudarte.</p>
            <Button 
              variant="outline" 
              size="lg" 
              className="bg-white text-blue-600 border-blue-600 hover:bg-blue-50"
              onClick={() => window.open('https://wa.me/5543746359', '_blank')}
            >
              <MessageCircle className="mr-2 h-5 w-5" />
              Chatea con nosotros en WhatsApp
            </Button>
            <div className="mt-8 flex justify-center space-x-6">
              <a href="https://www.instagram.com/cuidadoinfinito" target="_blank" rel="noopener noreferrer" className="text-white hover:text-blue-200">
                <Instagram className="h-8 w-8" />
                <span className="sr-only">Instagram</span>
              </a>
              <a href="https://www.facebook.com/cuidadoinfinito" target="_blank" rel="noopener noreferrer" className="text-white hover:text-blue-200">
                <Facebook className="h-8 w-8" />
                <span className="sr-only">Facebook</span>
              </a>
              <a href="https://www.tiktok.com/@cuidadoinfinito" target="_blank" rel="noopener noreferrer" className="text-white hover:text-blue-200">
                <TikTokIcon className="h-8 w-8" />
                <span className="sr-only">TikTok</span>
              </a>
            </div>
          </div>
        </section>
      </main>

      <footer className="bg-gray-800 text-white py-8">
        <div className="container mx-auto px-4 text-center">
          <p>&copy; 2023 Cuidado Infinito: 30 Años de Excelencia. Todos los derechos reservados.</p>
          <div className="mt-4 flex justify-center space-x-6">
            <a href="https://www.instagram.com/cuidadoinfinito" target="_blank" rel="noopener noreferrer" className="text-gray-400 hover:text-white">
              <Instagram className="h-6 w-6" />
              <span className="sr-only">Instagram</span>
            </a>
            <a href="https://www.facebook.com/cuidadoinfinito" target="_blank" rel="noopener noreferrer" className="text-gray-400 hover:text-white">
              <Facebook className="h-6 w-6" />
              <span className="sr-only">Facebook</span>
            </a>
            <a href="https://www.tiktok.com/@cuidadoinfinito" target="_blank" rel="noopener noreferrer" className="text-gray-400 hover:text-white">
              <TikTokIcon className="h-6 w-6" />
              <span className="sr-only">TikTok</span>
            </a>
          </div>
        </div>
      </footer>

      {/* Service Modal */}
      <Dialog open={isServiceModalOpen} onOpenChange={setIsServiceModalOpen}>
        <DialogContent className="sm:max-w-[700px]">
          <DialogHeader>
            <DialogTitle>{currentService}</DialogTitle>
            <DialogDescription>
              Descubre nuestras técnicas especializadas y consejos profesionales.
            </DialogDescription>
          </DialogHeader>
          <ScrollArea className="max-h-[60vh] overflow-y-auto">
            <div className="grid gap-6 py-4">
              {serviceTechniques[currentService as keyof typeof serviceTechniques]?.map((technique, index) => (
                <Card key={index}>
                  <CardHeader>
                    <CardTitle>{technique.title}</CardTitle>
                    <CardDescription>{technique.description}</CardDescription>
                  </CardHeader>
                  <CardContent>
                    <p className="text-sm text-muted-foreground"><strong>Consejo profesional:</strong> {technique.tip}</p>
                  </CardContent>
                </Card>
              ))}
            </div>
            {currentService === 'Restauración de Prendas' && (
              <div className="mt-8">
                <h4 className="text-lg font-semibold mb-4">Consejos para Reciclar y Donar Ropa</h4>
                <div className="grid gap-4">
                  {recyclingTips.map((tip, index) => (
                    <div key={index} className="flex items-start space-x-3">
                      <tip.icon className="w-6 h-6 text-blue-600 mt-1" />
                      <div>
                        <h5 className="font-medium">{tip.title}</h5>
                        <p className="text-sm text-muted-foreground">{tip.description}</p>
                      </div>
                    </div>
                  ))}
                </div>
              </div>
            )}
          </ScrollArea>
          <DialogFooter>
            <Button onClick={() => setIsServiceModalOpen(false)} className="bg-blue-600 hover:bg-blue-700 text-white">
              <ArrowLeft className="mr-2 h-4 w-4" />
              Volver a Servicios
            </Button>
          </DialogFooter>
        </DialogContent>
      </Dialog>

      {/* Order Modal */}
      <Dialog open={isOrderModalOpen} onOpenChange={setIsOrderModalOpen}>
        <DialogContent className="sm:max-w-[500px]">
          <DialogHeader>
            <DialogTitle>Haz tu pedido</DialogTitle>
            <DialogDescription>
              Completa el formulario para solicitar nuestro servicio de lavandería.
            </DialogDescription>
          </DialogHeader>
          <form onSubmit={handleOrderSubmit}>
            <div className="grid gap-4 py-4">
              <div className="grid grid-cols-4 items-center gap-4">
                <Label htmlFor="name" className="text-right">
                  Nombre
                </Label>
                <Input id="name" className="col-span-3" required />
              </div>
              <div className="grid grid-cols-4 items-center gap-4">
                <Label htmlFor="email" className="text-right">
                  Email
                </Label>
                <Input id="email" type="email" className="col-span-3" required />
              </div>
              <div className="grid grid-cols-4 items-center gap-4">
                <Label htmlFor="phone" className="text-right">
                  Teléfono
                </Label>
                <Input id="phone" type="tel" className="col-span-3" required />
              </div>
              <div className="grid grid-cols-4 items-center gap-4">
                <Label htmlFor="address" className="text-right">
                  Dirección
                </Label>
                <Input id="address" className="col-span-3" required />
              </div>
              <div className="grid grid-cols-4 items-center gap-4">
                <Label htmlFor="service" className="text-right">
                  Servicio
                </Label>
                <select id="service" value={selectedService} onChange={(e) => setSelectedService(e.target.value)} className="col-span-3">
                  <option value="">Selecciona un servicio</option>
                  {services.map(service => (
                    <option key={service.title} value={service.title}>{service.title}</option
))}
                </select>
              </div>
              <div className="flex justify-end mt-4">
                <Button type="submit" className="bg-blue-600 hover:bg-blue-700 text-white">
                  Enviar Pedido
                </Button>
              </div>
            </div>
          </form>
        </DialogContent>
      </Dialog>
    </div>
  )
}
