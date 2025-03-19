# Entregable--2
Entregable de nuestro blog de notas 

CREATE TABLE Usuarios (
    id INT PRIMARY KEY IDENTITY(1,1),
    nombre VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    contraseña NVARCHAR(MAX) NOT NULL,
    fecha_creacion DATETIME DEFAULT GETDATE()
);

CREATE TABLE Categorias (
    id INT PRIMARY KEY IDENTITY(1,1),
    nombre VARCHAR(50) UNIQUE NOT NULL
);

CREATE TABLE Carpetas (
    id INT PRIMARY KEY IDENTITY(1,1),
    usuario_id INT NOT NULL,
    nombre VARCHAR(100) NOT NULL,
    fecha_creacion DATETIME DEFAULT GETDATE(),
    FOREIGN KEY (usuario_id) REFERENCES Usuarios(id) ON DELETE CASCADE
);

CREATE TABLE Notas (
    id INT PRIMARY KEY IDENTITY(1,1),
    usuario_id INT NOT NULL,
    carpeta_id INT NULL,
    categoria_id INT NULL,
    titulo VARCHAR(200) NOT NULL,
    contenido NVARCHAR(MAX) NOT NULL,
    fecha_creacion DATETIME DEFAULT GETDATE(),
    FOREIGN KEY (usuario_id) REFERENCES Usuarios(id) ON DELETE CASCADE,
    FOREIGN KEY (carpeta_id) REFERENCES Carpetas(id) ON DELETE NO ACTION, 
    FOREIGN KEY (categoria_id) REFERENCES Categorias(id) ON DELETE SET NULL
);

CREATE TABLE Archivos (
    id INT PRIMARY KEY IDENTITY(1,1),
    usuario_id INT NOT NULL,
    carpeta_id INT NULL,
    nota_id INT NULL,
    nombre VARCHAR(255) NOT NULL,
    tipo VARCHAR(50) NOT NULL,
    datos VARBINARY(MAX) NOT NULL,
    fecha_subida DATETIME DEFAULT GETDATE(),
    FOREIGN KEY (usuario_id) REFERENCES Usuarios(id) ON DELETE CASCADE,
    FOREIGN KEY (carpeta_id) REFERENCES Carpetas(id) ON DELETE NO ACTION,
    FOREIGN KEY (nota_id) REFERENCES Notas(id) ON DELETE NO ACTION -- Evita el error de múltiples cascadas
);
