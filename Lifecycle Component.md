# Ciclo de Vida del Componente OWL

## setup

Hook: none

Descripción: Inicializa el componente configurando el estado y las propiedades. Este método se llama una vez, antes de que se realice cualquier renderizado o actualización. En setup, puedes definir el estado inicial, vincular datos reactivos, o preparar cualquier lógica que necesite estar lista antes de que el componente comience a interactuar con el usuario.

```javascript
import { Component, useState } from '@odoo/owl';

class MyComponent extends Component {
    setup() {
        this.state = useState({ count: 0 });
    }
}
```

## willStart

Hook: onWillStart

Descripción: Se utiliza para realizar tareas asíncronas antes del primer renderizado. Es ideal para inicializar datos que se necesitan para el primer renderizado del componente.

```javascript
import { Component, onWillStart } from '@odoo/owl';

class MyComponent extends Component {
  setup() {
    onWillStart(async () => {
      this.data = await fetchData();
    });
  }
}
```

## willRender

Hook: onWillRender

Descripción: Se llama justo antes de que el componente sea renderizado. Puedes utilizar este método para preparar cualquier dato o lógica que debe estar lista justo antes de que el componente se dibuje.

```javascript
import { Component, onWillRender } from '@odoo/owl';

class MyComponent extends Component {
  setup() {
    onWillRender(() => {
      console.log("Component will render");
    });
  }
}
```

## rendered

Hook: onRendered

Descripción: Se invoca justo después de que el componente ha sido renderizado. Puedes utilizar este método para realizar tareas que dependen de la existencia del DOM del componente, como la inicialización de librerías que interactúan con el DOM.

```javascript
import { Component, onRendered } from '@odoo/owl';

class MyComponent extends Component {
  setup() {
    onRendered(() => {
        console.log("Component has been rendered");
    });
  }
}
```

## mounted

Hook: onMounted

Descripción: Se llama después de que el componente ha sido renderizado y agregado al DOM. Es útil para realizar manipulaciones del DOM o inicializar integraciones que requieran que el componente esté completamente en el DOM.

```javascript
import { Component, onMounted } from '@odoo/owl';

class MyComponent extends Component {
  setup() {
    onMounted(() => {
      this.el.querySelector('button').addEventListener('click', this.increment.bind(this));
    });
  }
}
```

## willUpdateProps

Hook: onWillUpdateProps

Descripción: Se invoca antes de que se actualicen las propiedades del componente. Aquí puedes implementar lógica que reaccione a cambios en las propiedades antes de que el componente se vuelva a renderizar.

```javascript
import { Component, onWillUpdateProps } from '@odoo/owl';

class MyComponent extends Component {
  setup() {
    onWillUpdateProps(nextProps => {
      return this.loadData({id: nextProps.id});
    });
  }
}
```

## willPatch

Hook: onWillPatch

Descripción: Se llama justo antes de que el DOM sea parcheado con los nuevos datos. Puedes usar este método para preparar cualquier cambio en el DOM que necesite ser manejado justo antes de que OWL aplique las diferencias al DOM.

```javascript
import { Component, onWillPatch } from '@odoo/owl';

class MyComponent extends Component {
  setup() {
    onWillPatch(() => {
      this.scrollState = this.getScrollSTate();
    });
  }
}
```

## patched

Hook: onPatched

Descripción: Se invoca justo después de que el DOM ha sido parcheado. Es útil para realizar ajustes finales o reacciones a la actualización del DOM.

```javascript
import { Component, onPatched } from '@odoo/owl';

class MyComponent extends Component {
  setup() {
    onPatched(() => {
      this.scrollState = this.getScrollState();
    });
  }
}
```

## willUnmount

Hook: onWillUnmount

Descripción: Se utiliza justo antes de que el componente sea eliminado del DOM. Es ideal para limpiar recursos o escuchadores de eventos que fueron configurados durante el ciclo de vida del componente.

```javascript
import { Component, onWillUnmount } from '@odoo/owl';

class MyComponent extends Component {
  setup() {
    onWillUnmount(() => {
        this.el.querySelector('button').removeEventListener('click', this.increment.bind(this));
    });
  }
}
```

##  willDestroy

Hook: onWillDestroy

Descripción: Se llama justo antes de que el componente sea destruido. Aquí puedes limpiar cualquier recurso que el componente haya creado o administrado, como conexiones a bases de datos, suscripciones, etc.

```javascript
import { Component, onWillDestroy } from '@odoo/owl';

class MyComponent extends Component {
   setup() {
    onWillDestroy(() => {
      console.log("Component will be destroyed");
    });
  }
}
```

##  error

Hook: onError

Descripción: Maneja errores que se producen durante el ciclo de vida del componente. Puedes usar este método para capturar y manejar errores de manera global en el componente.

```javascript
import { Component, onError } from '@odoo/owl';

class MyComponent extends owl.Component {
  onError(() => {
    console.error("An error occurred:", error);
  });
}
```
