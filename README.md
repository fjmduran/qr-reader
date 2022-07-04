# Lector QR con Angular 13

Este ejemplo de realizar un lector de códigos QR o código de barra con Angular 13 es muy rápido.

He tardado un par de horas de descubrir cómo poder seleccionar la cámara y ese es el motivo de hacer este repositorio.

Para ejecutarlo, cuando tengas clonado el repositorio ejecuta ``npm install``

![screenshot de la aplicación de lector de código QR en Angular 13](https://github.com/fjmduran/qr-reader/blob/master/src/assets/img.jpg?raw=true)

Uso la versión 3.5.0 de la librería [ngx-scanner](https://github.com/zxing-js/ngx-scanner)

Para obtener los periféricos de captura de imagen de tu dispositivo puedes ejecutar:

    navigator.mediaDevices.enumerateDevices().then((devices) => {
      for (var i = 0; i < devices.length; i++) {
        var device = devices[i];
        if (device.kind === 'videoinput') {
          console.log(device);
          this.myDevice = devices[1];          
        }
      }
      console.log(this.myDevice);
    });

No obstante la librería ya te facilita el método ``camerasFound``

Aquí tienes todas las propiedas del componente:

    <zxing-scanner
    [enable]="scannerEnabled" 
    [(device)]="desiredDevice"
    [torch]="torch"
    (torchCompatible)="onTorchCompatible($event)"
    (camerasFound)="camerasFoundHandler($event)"
    (camerasNotFound)="camerasNotFoundHandler($event)"
    (scanSuccess)="scanSuccessHandler($event)"
    (scanError)="scanErrorHandler($event)"
    (scanFailure)="scanFailureHandler($event)"
    (scanComplete)="scanCompleteHandler($event)"
    ></zxing-scanner>


enable->Starts and Stops the scanning.

autofocusEnabledue->Not working at the moment, needs ImageCapture API implementation.

device->The video-device used for scanning (use one of the devices emitted by camerasFound), it can be set or emit some value.

torch->Can turn on/off the device flashlight.

torchCompatible->Tells if the device's torch is compatible w/ the scanner.

camerasFound->Emits an array of video-devices after view was initialized.
camerasNotFound->Emits a void event when cameras aren't found.
scanSuccess->Emits the result as string, after a valid QR code was scanned.

scanError->Emitted when some error occurs during the scan process.

scanFailure->Emitted when the scanner couldn't decode any result from the media stream.

scanComplete->Emitted after any scan attempt, no matter what.
