# BD-PuntoVenta

CREATE DATABASE IF NOT EXISTS puntoventa;
USE puntoventa;

-- Tabla `mensajes enviados`
CREATE TABLE `mensajes_enviados` (
  `id_mensaje` int(11) NOT NULL AUTO_INCREMENT,
  `id_cliente` int(11) NOT NULL,
  `contenido` text NOT NULL,
  `fecha` date NOT NULL,
  PRIMARY KEY (`id_mensaje`),
  FOREIGN KEY (`id_cliente`) REFERENCES `tb_clientes` (`id_cliente`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Tabla `mensajes recibidos`
CREATE TABLE `mensajes_recibidos` (
  `id_mensaje` int(11) NOT NULL AUTO_INCREMENT,
  `id_cliente` int(11) NOT NULL,
  `contenido` varchar(500) NOT NULL,
  `fecha` date NOT NULL,
  `nombre` varchar(100) NOT NULL,
  PRIMARY KEY (`id_mensaje`),
  FOREIGN KEY (`id_cliente`) REFERENCES `tb_clientes` (`id_cliente`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Tabla `tb_clientes`
CREATE TABLE `tb_clientes` (
  `id_cliente` int(11) NOT NULL AUTO_INCREMENT,
  `nom_cliente` varchar(50) NOT NULL,
  `correo` varchar(30) NOT NULL,
  `direccion` varchar(60) NOT NULL,
  `telefono` varchar(10) NOT NULL,
  `rfc` varchar(13) NOT NULL,
  PRIMARY KEY (`id_cliente`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Tabla `tb_detalle_pedidos`
CREATE TABLE `tb_detalle_pedidos` (
  `id_detalle` int(11) NOT NULL AUTO_INCREMENT,
  `id_pedido` int(11) NOT NULL,
  `id_producto` int(11) NOT NULL,
  `cantidad` int(11) NOT NULL,
  PRIMARY KEY (`id_detalle`),
  FOREIGN KEY (`id_pedido`) REFERENCES `tb_pedidos` (`id_pedido`) ON DELETE CASCADE,
  FOREIGN KEY (`id_producto`) REFERENCES `tb_productos` (`id_producto`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Tabla `tb_galeria`
CREATE TABLE `tb_galeria` (
  `id_imagen` int(11) NOT NULL AUTO_INCREMENT,
  `titulo` varchar(20) NOT NULL,
  `descripcion` varchar(100) DEFAULT NULL,
  `imagenRuta` varchar(100) NOT NULL,
  PRIMARY KEY (`id_imagen`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Tabla `tb_materiales`
CREATE TABLE `tb_materiales` (
  `id_material` int(11) NOT NULL AUTO_INCREMENT,
  `descripcion` varchar(20) NOT NULL,
  `existencias` int(11) NOT NULL,
  `cantidad_minima` int(11) NOT NULL,
  `unidad` varchar(8) NOT NULL,
  `id_proveedor` int(11) NOT NULL,
  PRIMARY KEY (`id_material`),
  FOREIGN KEY (`id_proveedor`) REFERENCES `tb_proveedores` (`id_proveedor`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Tabla `tb_pedidos`
CREATE TABLE `tb_pedidos` (
  `id_pedido` int(11) NOT NULL AUTO_INCREMENT,
  `id_cliente` int(11) NOT NULL,
  `id_usuario` int(11) NOT NULL,
  `fecha` date NOT NULL,
  `monto` double NOT NULL,
  `estatus` varchar(10) NOT NULL,
  PRIMARY KEY (`id_pedido`),
  FOREIGN KEY (`id_cliente`) REFERENCES `tb_clientes` (`id_cliente`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Tabla `tb_productos`
CREATE TABLE `tb_productos` (
  `id_producto` int(11) NOT NULL AUTO_INCREMENT,
  `descripcion` varchar(30) NOT NULL,
  `tamano` varchar(8) NOT NULL,
  `color` varchar(10) NOT NULL,
  `id_tipo` int(11) NOT NULL,
  `imagen` varchar(80) NOT NULL,
  `precio_mayoreo` double NOT NULL,
  `precio_menudeo` double NOT NULL,
  `existencias` int(11) NOT NULL,
  PRIMARY KEY (`id_producto`),
  FOREIGN KEY (`id_tipo`) REFERENCES `tb_tipos` (`id_tipo`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Tabla `tb_proveedores`
CREATE TABLE `tb_proveedores` (
  `id_proveedor` int(11) NOT NULL AUTO_INCREMENT,
  `nom_proveedor` varchar(50) NOT NULL,
  `correo` varchar(30) NOT NULL,
  `telefono` varchar(10) NOT NULL,
  PRIMARY KEY (`id_proveedor`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Tabla `tb_tipos`
CREATE TABLE `tb_tipos` (
  `id_tipo` int(11) NOT NULL AUTO_INCREMENT,
  `tipo` varchar(15) NOT NULL,
  PRIMARY KEY (`id_tipo`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Tabla `tb_usuarios`
CREATE TABLE `tb_usuarios` (
  `id_usuario` int(11) NOT NULL AUTO_INCREMENT,
  `nom_usuario` varchar(10) NOT NULL,
  `clave` varchar(8) NOT NULL,
  `correo` varchar(30) NOT NULL,
  PRIMARY KEY (`id_usuario`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_general_ci;

-- Insertar datos en las tablas según sea necesario...


-- Insertar datos en las tablas

-- Datos para la tabla `tb_clientes`
INSERT INTO `tb_clientes` (`id_cliente`, `nom_cliente`, `correo`, `direccion`, `telefono`, `rfc`) VALUES
(1, 'lizz', 'agar.iopoker985@gmail.com', 'CELAYA 3', '4181435821', 'RASO990221PP2');

-- Datos para la tabla `tb_materiales`
INSERT INTO `tb_materiales` (`id_material`, `descripcion`, `existencias`, `cantidad_minima`, `unidad`, `id_proveedor`) VALUES
(1, 'pasta', 26, 10, 'bultos', 2),
(2, 'color rojo', 2, 2, 'kilo(s)', 1),
(3, 'color naranja', 4, 2, 'kilos (s', 1),
(4, 'molde juego#40', 10, 5, 'moldes', 5);

-- Datos para la tabla `tb_proveedores`
INSERT INTO `tb_proveedores` (`id_proveedor`, `nom_proveedor`, `correo`, `telefono`) VALUES
(1, 'EuroColor', 'eurocolor@gmail.com', '4181818181'),
(2, 'Materiales Alejandra', 'alejandra@gmail.com', '4181827966'),
(3, 'ExpressNieto', 'gas@gmail.com', '4188778752'),
(4, 'procerama', 'procerama@gmaiul.com', '4788585862'),
(5, 'Moldes Nicolas', 'moldes@gmail.com', '6667878215');

-- Datos para la tabla `tb_tipos`
INSERT INTO `tb_tipos` (`id_tipo`, `tipo`) VALUES
(1, 'Jarrones'),
(2, 'Vajillas'),
(3, 'Decoraciones'),
(4, 'Platos'),
(5, 'Macetas'),
(6, 'Cazuelas'),
(7, 'Ollas'),
(8, 'Tazas'),
(9, 'Lamparas');

-- Datos para la tabla `tb_usuarios`
INSERT INTO `tb_usuarios` (`id_usuario`, `nom_usuario`, `clave`, `correo`) VALUES
(1, 'Oscar', 'linux', 'oscar@ceramica.com'),
(2, 'Maribel', 'linux', 'maribel@ceramica.com'),
(3, 'Josue', 'linux', 'josue@ceramica.com'),
(4, 'Noah', 'linux', 'noah@ceramica.com');
