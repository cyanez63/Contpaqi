# Contpaqi

Este proyecto incluye clases listas para conectarse al SDK de Adminpaq y Comercial.

Tambien incluye unas clases para conectarse directamente a la base de datos de los sistemas de Contabilidad y Comercial usando Entity Framework.

Es importante saber que no todas las funciones en las clases del SDK tienen los parametros correctos dado a que no es facil saber si un char* es de tipo string o StringBuilder, o cuales parametros deben ser por referencia.

Si encuentran parametros incorrectos o funciones faltantes porfavor dejenmelo saber.

Esta libreria la uso para todos mis proyectos y es la base para otras librerias que uso y pense pudiera ser de ayuda o otros desarrolladores.

Tratare de incluir ejemplos de como usar la libreria despues.

# Comercial
## Como inicializar el SDK de Comercial

```csharp
using Contpaqi.SistemasComerciales.Sdk;
using Contpaqi.SistemasComerciales.Sdk.Extras;
using System.Text;

namespace Comercial
{
     class Program
    {
        static void Main(string[] args)
        {
            int contpaqResult = 1; // 0 = exito. > 0 = error
            contpaqResult = InicializacionComercialSdk.InicializarSDK();
            if (contpaqResult != 0)
            {
                Console.WriteLine(ErroresComercial.LeerError(contpaqResult));
            }
            else
            {
                ComercialSdk.fTerminaSDK();
            }
        }
    }
}
```

## Como utilizar el SDK de Comercial

```csharp
using Contpaqi.SistemasComerciales.Sdk;
using Contpaqi.SistemasComerciales.Sdk.Extras;
using System.Text;

namespace Comercial
{
     class Program
    {
        static void Main(string[] args)
        {
            int contpaqResult = 1; // 0 = exito. > 0 = error
            contpaqResult = InicializacionComercialSdk.InicializarSDK();
            if (contpaqResult != 0)
            {
                System.Console.WriteLine(ErroresComercial.LeerError(contpaqResult));
            }
            else
            {
                int empresaId = 0;
                StringBuilder nombre = new StringBuilder(ComercialSdk.kLongNombre);
                StringBuilder ruta = new StringBuilder(ComercialSdk.kLongRuta);
                contpaqResult = ComercialSdk.fPosPrimerEmpresa(ref empresaId, nombre, ruta);
                System.Console.WriteLine($"Id {empresaId} Nombre {nombre} Ruta{ruta}");
                do
                {
                    empresaId = 0;
                    nombre = new StringBuilder(ComercialSdk.kLongNombre);
                    ruta = new StringBuilder(ComercialSdk.kLongRuta);
                    int isFinDeLaTabla = ComercialSdk.fPosSiguienteEmpresa(ref empresaId, nombre, ruta);
                    if (isFinDeLaTabla != 0)
                    {
                        break;
                    }
                    System.Console.WriteLine($"{empresaId} {nombre} | {ruta}");
                } while (true);
                ComercialSdk.fTerminaSDK();
            }
        }
    }
}
```

# Adminpaq
## Como inicializar el SDK de Adminpaq

```csharp
using Contpaqi.SistemasComerciales.Sdk;
using Contpaqi.SistemasComerciales.Sdk.Extras;
using System.Text;

namespace Adminpaq
{
     class Program
    {
        static void Main(string[] args)
        {
            int contpaqResult = 1; // 0 = exito. > 0 = error
            contpaqResult = InicializacionAdminpaqSdk.InicializarSDK();
            if (contpaqResult != 0)
            {
                System.Console.WriteLine(ErroresAdminpaq.LeerError(contpaqResult));
            }
            else
            {
                AdminpaqSdk.fTerminaSDK();
            }
        }
    }
}
```

## Como utilizar el SDK de Adminpaq

```csharp
using Contpaqi.SistemasComerciales.Sdk;
using Contpaqi.SistemasComerciales.Sdk.Extras;
using System.Text;

namespace Adminpaq
{
     class Program
    {
        static void Main(string[] args)
        {
            int contpaqResult = 1; // 0 = exito. > 0 = error
            contpaqResult = InicializacionAdminpaqSdk.InicializarSDK();
            if (contpaqResult != 0)
            {
                System.Console.WriteLine(ErroresAdminpaq.LeerError(contpaqResult));
            }
            else
            {
                int empresaId = 0;
                StringBuilder nombre = new StringBuilder(AdminpaqSdk.kLongNombre);
                StringBuilder ruta = new StringBuilder(AdminpaqSdk.kLongRuta);
                contpaqResult = AdminpaqSdk.fPosPrimerEmpresa(ref empresaId, nombre, ruta);
                System.Console.WriteLine($"Id {empresaId} Nombre {nombre} Ruta{ruta}");
                do
                {
                    empresaId = 0;
                    nombre = new StringBuilder(AdminpaqSdk.kLongNombre);
                    ruta = new StringBuilder(AdminpaqSdk.kLongRuta);
                    int isFinDeLaTabla = AdminpaqSdk.fPosSiguienteEmpresa(ref empresaId, nombre, ruta);
                    if (isFinDeLaTabla != 0)
                    {
                        break;
                    }
                    System.Console.WriteLine($"{empresaId} {nombre} | {ruta}");
                } while (true);
                AdminpaqSdk.fTerminaSDK();
            }
        }
    }
}
```
